[How to Design a Hotel Booking System?](https://javascript.plainenglish.io/how-to-design-a-hotel-booking-system-56ef18b6adfc)
=====================================

(e.g Airbnb, Booking, Expedia from a front-end/full-stack view)
---------------------------------------------------------------

[![Leanne Z](https://miro.medium.com/v2/resize:fill:88:88/2*6hvhJMsNdJ2MWbPuIJqTug.jpeg)](https://leannezhang.medium.com/?source=post_page-----56ef18b6adfc--------------------------------)
[![JavaScript in Plain English](https://miro.medium.com/v2/resize:fill:48:48/1*yUNfohs9jA6GCDmyCYJTvA@2x.png)](https://javascript.plainenglish.io/?source=post_page-----56ef18b6adfc--------------------------------)

[Leanne Z](https://leannezhang.medium.com/?source=post_page-----56ef18b6adfc--------------------------------)

Follow 1,071

My step-by-step approach
------------------------

This is one of the front-end system design questions I will be working on. Stay tuned for more interview system design questions I did from [Great Front](https://www.greatfrontend.com/?fpr=leanne83)end, or [Exponent](https://www.tryexponent.com/?ref=mgu1mwy).

![](https://miro.medium.com/v2/resize:fit:700/1*xIeqz1WhQw8mlpBtV29FsA.png)

**1. Define the functional and non-functional requirements.**
---------------------------------------------------------

*Target audience: front-end / full-stack engineer*

![](https://miro.medium.com/v2/resize:fit:1000/1*xqei3fddp7GK98INRQRc0g.png)

![](https://miro.medium.com/v2/resize:fit:1000/1*kKyzSlFvJJfV6dOOqW7RZQ.png)

![](https://miro.medium.com/v2/resize:fit:700/1*uBX0t0RW1yvtfJ1YQro-3A.png)

Rough sketch mockup for front-end to identify common UI components

We can use ReactJs, Redux, and React-query to hold states and fetch data.

Re-usable React Components can be the following:

1.  SearchBar
2.  FilterBar
3.  ImageCarousel
4.  StarRatingWidget
5.  MapView

**2. Define APIs**
--------------

-   `GET /hotels`: View all hotels by preselected location
-   `GET /hotels/{hotel_id}`: View hotel details
-   `POST /reservations`: Make a hotel reservation
-   `POST /payments`: Make a payment

![](https://miro.medium.com/v2/resize:fit:700/1*psAsrtQg6zCVxrIBaR48GA.png)

APIs Requests and Responses
---------------------------

-   GET /hotels: can filter by price, room type, amenities, pagination, and sort. Return a list of hotels
-   POST /reservations: make a reservation with the guest name once payment is successful

![](https://miro.medium.com/v2/resize:fit:1000/1*SlttPbHSpP-v-rylUS71Hg.png)

**3. Define Data Model**
--------------------

We can build the models below using relational databases like Postgres.

![](https://miro.medium.com/v2/resize:fit:700/1*RHw1mE7wPnQbzE0Hje-NFg.png)

**4. Define High-Level System (Iteration 1)**
------------------------------------------

We will build services into microservices. Each microservice calls its database.

-   Guest Service which handles information for the logged user
-   Inventory Service which shows available hotels
-   Reservation Service which handles booking a hotel
-   Payment Service: we will be using 3rd party service like Stripe

![](https://miro.medium.com/v2/resize:fit:700/1*C3ulvuc_c97sJRpY_kVj7g.png)

**5. How can we improve and optimize the system?**
----------------------------------------------

![](https://miro.medium.com/v2/resize:fit:1000/1*cg-MxpKFISljAjXimrYJ1w.png)

System Level Optimizations:
---------------------------

-   Images can be stored in an S3 bucket which can be cached through CDN
-   Cached previous database results before calling the database again
-   Cached commonly popular hotels before going to the server
-   Cached last viewed hotels

UI Performance Optimizations:
-----------------------------

-   use React-Query to cache recent API requests from users
-   auto pre-fetch content before the next page or image is selected
-   support pagination for /GET requests
-   load images in different sizes by the viewport. Can fetch smaller size image of the viewport is small for responsive design
-   user debounce() when searching to prevent too many requests from fetching
-   make of useCallback() and useMemo() in React Components

Finally, save this diagram below👇
==================================

*Be sure to **subscribe** to my *[*Youtube Channel*](http://codingbff/)* for upcoming in-depth systems design videos.*

*C️️omment and clap if you like this post **️👏*

-   Follow me: [YouTube](http://codingbff/) | [LinkedIn](https://www.linkedin.com/in/leannezhang/) | [Substack](https://leannez.substack.com/)
-   For more front-end system design practice, you can sign up [GreatFrontend](https://www.greatfrontend.com/?fpr=leanne83)

![](https://miro.medium.com/v2/resize:fit:1000/1*Ld0X5NPFl0lgkvyss4gJ5w.png)

In Plain English 🚀
===================

*Thank you for being a part of the *[*In Plain English*](https://plainenglish.io/)* community! Before you go:*

-   Be sure to clap and follow the writer ️👏️️
-   More content at [PlainEnglish.io](https://plainenglish.io/)