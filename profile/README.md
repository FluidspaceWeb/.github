<div align="center">
  <img src="https://github.com/FluidspaceWeb/.github/assets/25845504/0525ccb4-bfcf-4db4-95bf-a871b32bb07d" width="800">
</div>

<h3 align="center">
	<a href="https://fluidspace.app">Website</a>
	<span> | </span>
	<a href="https://discord.gg/reeUqaDb2v">Discord</a>
	<span> | </span>
  <a href="https://www.youtube.com/@FluidspaceApp">YouTube</a>
  <span> | </span>
	<a href="https://www.instagram.com/fluidspace.app/">Instagram</a>
	<span> | </span>
	<a href="https://twitter.com/FluidspaceApp">Twitter(X)</a>
</h3>
<hr>

# What is Fluidspace?

[Fluidspace](https://fluidspace.app) is a web environment to host custom-made tools for businesses and developers. Fluidspace out-of-the-box provides Auth, Role based access control (RBAC), Real-time events, Multi-tenancy, Data bucketing and 3rd party integration support (via its REST API).

Users can create multiple Spaces under their account/subscription, each Space can theoretically have unlimited number of users and pages. These pages contain modules which are the custom-made tools inside a [Shadow DOM](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM) isolated from rest of the environment and modules.

<details>
  <summary>Expand to see end-user web interface</summary>
  <div align="center">
    <img src="https://github.com/FluidspaceWeb/.github/assets/25845504/132b5ab1-b110-4f3d-ba80-8beca8a76683" width="800">
  </div>
</details>

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
* Use [App](https://github.com/FluidspaceWeb/app-template-vue3) or [Integration](https://github.com/FluidspaceWeb/integration-template-vue3) template as base to get started.
