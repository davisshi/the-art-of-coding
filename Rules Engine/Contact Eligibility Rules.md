```[](https://)Java
package drools.kierule;

import com.prudential.consent.management.constant.ConsentStatus;
import com.prudential.consent.management.dto.ContactEligibilityDto;
import org.apache.commons.collections.CollectionUtils;
import com.prudential.consent.management.constant.Constants;

global com.prudential.consent.management.service.impl.ContactEligibilityServiceImpl contactEligibilityService;
dialect "mvel"

rule "Is there a phone number"
    when
        contactEligibilityObject: ContactEligibilityDto(phoneNum == null);
    then
        modify(contactEligibilityObject) {
                setContactEligibility(Boolean.FALSE)
        };
        contactEligibilityObject.getComments().add("There is no phone number");
end

rule "Is that phone number valid"
    when
        contactEligibilityObject: ContactEligibilityDto(
            contactEligibility == null
            && (isValidPhoneNum == null || isValidPhoneNum == Boolean.FALSE)
        );
    then
        modify(contactEligibilityObject) {
                setContactEligibility(Boolean.FALSE)
        };
        contactEligibilityObject.getComments().add("Phone number is not valid");
end

rule "Phone number is not a mobile number, and not on a Federal or State DNC list, then can contact"
    when
        contactEligibilityObject: ContactEligibilityDto(
            contactEligibility == null
            && isMobilePhoneNum == Boolean.FALSE
            && federalDNCDate == null
            && CollectionUtils.isEmpty(stateDNCDates)
        );
    then
        modify(contactEligibilityObject) {
                setContactEligibility(Boolean.TRUE)
        };
        contactEligibilityObject.getComments().add("Phone number is not a mobile number");
        contactEligibilityObject.getComments().add("Phone number is not on a Federal or State DNC list");
end

rule "Phone number is not a mobile number, is on a Federal or State DNC list, and we don't have consent to call the number"
    when
        contactEligibilityObject: ContactEligibilityDto(
            contactEligibility == null
            && isMobilePhoneNum == Boolean.FALSE
            && (federalDNCDate != null || !CollectionUtils.isEmpty(stateDNCDates))
            && latestConsentStatus != ConsentStatus.ACCEPTED
        );
    then
        modify(contactEligibilityObject) {
                setContactEligibility(Boolean.FALSE)
        };
        contactEligibilityObject.getComments().add("Phone number is not a mobile number");
        contactEligibilityObject.getComments().add("Phone number is on Federal or State DNC list");
        contactEligibilityObject.getComments().add("We don't have consent to call the number");
end

rule "Phone number is a mobile number, we don't have consent to call the number, then cannot contact"
    when
        contactEligibilityObject: ContactEligibilityDto(
            contactEligibility == null
            && isMobilePhoneNum == Boolean.TRUE
            && latestConsentStatus != ConsentStatus.ACCEPTED
        );
    then
        modify(contactEligibilityObject) {
                setContactEligibility(Boolean.FALSE)
        };
        contactEligibilityObject.getComments().add("Phone number is a mobile number");
        contactEligibilityObject.getComments().add("We don't have consent to call the number");
end

rule "We have consent to call the number, user is a WSG customer, consent doesn't override permissions, and there is no permitted plan, then cannot contact"
    when
        contactEligibilityObject: ContactEligibilityDto(
            contactEligibility == null
            && latestConsentStatus == ConsentStatus.ACCEPTED
            && hasRetirementAccount == Boolean.TRUE
            && isOverridePermissions == Boolean.FALSE
            && hasPermittedPlan == Boolean.FALSE
        );
    then
        modify(contactEligibilityObject) {
                setContactEligibility(Boolean.FALSE)
        };
        contactEligibilityObject.getComments().add("We have consent to call the number");
        contactEligibilityObject.getComments().add("User is a WSG customer");
        contactEligibilityObject.getComments().add("Consent doesn't override permissions");
        contactEligibilityObject.getComments().add("There is no permitted plan");
end

rule "The number is on a Pru DNC list, and the entry in the Pru DNC is more recent than the consent, then cannot contact"
    when
        contactEligibilityObject: ContactEligibilityDto(
            contactEligibility == null
            && isNumberOnPruDNCList == Boolean.TRUE
            && isPruDNCNewerThanConsent == Boolean.TRUE
        );
    then
        modify(contactEligibilityObject) {
                setContactEligibility(Boolean.FALSE)
        };
        contactEligibilityObject.getComments().add("The number is on a Pru DNC list");
        contactEligibilityObject.getComments().add("The entry in the Pru DNC is more recent than the consent");
end

rule "The consent is not older than 45 days, then can contact"
    when
        contactEligibilityObject: ContactEligibilityDto(
            contactEligibility == null
            && consentDays <= Constants.CONSENT_DAYS_NEED_PHONEVERIFICATION
        );
    then
        modify(contactEligibilityObject) {
                setContactEligibility(Boolean.TRUE)
        };
        contactEligibilityObject.getComments().add("The consent is not older than 45 days");
end

rule "The consent is older than 45 days, then trigger to call phone number verification API"
    when
        contactEligibilityObject: ContactEligibilityDto(
            contactEligibility == null
            && consentDays > Constants.CONSENT_DAYS_NEED_PHONEVERIFICATION
        );
    then
        contactEligibilityService.verifyPhoneNumber(contactEligibilityObject);
        contactEligibilityObject.getComments().add("Phone number verification API was called");
        modify(contactEligibilityObject) {
            setIsStillOwnedByTheSamePersonWhoGaveConsent(contactEligibilityObject.getIsStillOwnedByTheSamePersonWhoGaveConsent())
        };
end

rule "The consent is older than 45 days, and the number is not still owned by the same person who gave consent, then cannot contact"
    when
        contactEligibilityObject: ContactEligibilityDto(
            contactEligibility == null
            && consentDays > Constants.CONSENT_DAYS_NEED_PHONEVERIFICATION
            && isStillOwnedByTheSamePersonWhoGaveConsent == Boolean.FALSE
        );
    then
        modify(contactEligibilityObject) {
                setContactEligibility(Boolean.FALSE)
        };
        contactEligibilityObject.getComments().add("The consent is older than 45 days");
        contactEligibilityObject.getComments().add("The number is not still owned by the same person who gave consent");
end

rule "The consent is older than 45 days, and the number is still owned by the same person who gave consent, then can contact"
    when
        contactEligibilityObject: ContactEligibilityDto(
            contactEligibility == null
            && consentDays > Constants.CONSENT_DAYS_NEED_PHONEVERIFICATION
            && isStillOwnedByTheSamePersonWhoGaveConsent == Boolean.TRUE
        );
    then
        modify(contactEligibilityObject) {
                setContactEligibility(Boolean.TRUE)
        };
        contactEligibilityObject.getComments().add("The consent is older than 45 days");
        contactEligibilityObject.getComments().add("The number is still owned by the same person who gave consent");
end
```
