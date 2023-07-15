# What is Fluidspace?

[Fluidspace](https://fluidspace.app) is a web environment to host custom-made tools for businesses and developers. Fluidspace out-of-the-box provides Auth, Role based access control (RBAC), Real-time events, Multi-tenancy, Data bucketing and 3rd party integration support (via its REST API).

Users can create multiple Spaces under their account/subscription, each Space can theoretically have unlimited number of users and pages. These pages contain modules which are the custom-made tools inside a [Shadow DOM](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM) isolated from rest of the environment and modules.

[Jump to Module Development Kit ⤵](#-module-development-kit)

## 🧩 Types of Module

* **App**<br>
These modules use database provided by Fluidspace to store all its data and access the data via DataAPI and PropsAPI. The data can be bucketed by the user with a concept termed *dataset*. The environment does not provide 3rd party (external) request controller but can be self-implemented by correct use of `fetch()` and PropsAPI. 

* **Integration**<br>
These modules use data from 3rd party sources via its REST API and have no access to the local database. Fluidspace handles adding of OAuth2 accounts and supports multiple account logins. The `refresh_token` is stored in database and used automatically to refresh the `access_token`.

## 📄 Page

A Space consists of pages, these pages visually encapsulate modules.

> **Visual Hierarchy:** Account > Space > Page(role dependent) > Module

Pages are role dependent, meaning they follow the permission level granted to the user by means of their role in Fluidspace. The permission levels are:

* (code: 0) Hidden
* (code: 1) View only
* (code: 4) View, Insert, Update
* (code: 9) View, Insert, Update, Delete

The modules inherit page permission in which they are encapsulated and, generally show different UI components based on the degree of permission available.

*Example: A button to insert/create data in a module shall be visible only if permission >= 1.*

## 🗄 Dataset

Fluidspace supports data bucketing in the name of **dataset**.

> **Data Hierarchy:** Subscription/Account > Dataset > Module

Datasets are user-defined virtual groups within the subscription for the overall accumulated user-data in the database. The datasets are shared among the modules and available to be used in all the Spaces that were created in your subscription. The datasets are selected at the module-level to specify its data source & grouping.

This nature of dataset enables you to create Space which sources data from various datasets, either:
* by having **same module** on **multiple pages** with different datasets or,
* by having **different module** on **same/multiple pages** with different datasets.

The real-time events for data changes are dispatched at the dataset level and propagated to all the Spaces that contain module using the respective dataset.

Note: Datasets are NOT shared with Spaces that you joined but are not created under your subscription.


## 🧑‍💻 Module Development Kit

* Setup the  [Development server](https://github.com/FluidspaceWeb/development-server) locally using docker for backend simulation.
* Use [App module template](https://github.com/FluidspaceWeb/app-template-vue3) as base to get started.