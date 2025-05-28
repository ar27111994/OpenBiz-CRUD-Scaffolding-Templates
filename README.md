# ASP.NET MVC CRUD Scaffolding Templates with AJAX Modals

## Introduction

These T4 scaffolding templates are designed for ASP.NET MVC and Entity Framework 6. Their purpose is to enable the rapid generation of feature-rich CRUD (Create, Read, Update, Delete) interfaces. Key characteristics of the generated interfaces include an AJAX-powered data grid and modal forms for creating and editing data. The templates are based on a generic repository pattern.

## Overview

**Project Context/Dependency Note:** These templates are designed to work optimally within a project structure that includes specific components and namespaces. Notably, dependencies such as `SCMS.ViewModels.PagedList` for pagination and `DAL.Repository.Persistence.IEntityService` for data access (or similarly named/structured components) are expected for full functionality. Please ensure your project incorporates these or equivalent structures for seamless integration.

## Table of Contents

*   [Introduction](#introduction)
*   [Overview](#overview)
*   [Table of Contents](#table-of-contents)
*   [Prerequisites/Dependencies](#prerequisitesdependencies)
*   [Key Features](#key-features)
*   [Installation and Setup](#installation-and-setup)
*   [How to Use](#how-to-use)
*   [Customization Notes](#customization-notes)
*   [Project Structure Expectation](#project-structure-expectation)
*   [License](#license)

## Prerequisites/Dependencies

Before using these templates, ensure your development environment and project include the following components:

**Core Frameworks & Tools:**

*   **ASP.NET MVC:** Version 5 is recommended.
*   **Entity Framework:** Version 6.x.
*   **.NET Framework:** Version 4.5 or later.
*   **Visual Studio:** VS 2015 or later is recommended to ensure compatibility with the latest T4 template features and scaffolding mechanisms. VS 2012/2013 might work but could require adjustments.

**Project-Specific Libraries & Namespaces (Crucial for Full Functionality):**

It's essential that your project incorporates the following (or similarly structured and named) components. The templates are designed to interact with these specific interfaces and classes.

*   **Data Access Layer (DAL):**
    *   `DAL.Repository.Persistence.IEntityService<T>`: Interface for the generic repository.
    *   `DAL.Repository.Persistence.EntityService<T>`: Implementation of the generic repository.
*   **View Models:**
    *   `SCMS.ViewModels.PagedList<T>`: Used for implementing pagination in the data grid.
*   **Data Export Utilities:**
    *   `SCMS.DataExport.ExcelFormatter`: Helper class for formatting data into Excel.
    *   `SCMS.DataExport.CsvResult`: Custom `ActionResult` for returning CSV data.
    *   `SCMS.Actions.ExcelResult`: Custom `ActionResult` for returning Excel files.
*   **Entity Framework DbContext:**
    *   A class named `SCMSContext` (or your project's equivalent DbContext, e.g., `ApplicationDbContext`) that inherits from `DbContext`. The templates will look for this to interact with your database.

**Client-Side Libraries (Typically managed via NuGet or included in `Scripts` and `Content` folders):**

*   **jQuery:** Version 1.10+ (or a version compatible with your chosen Bootstrap 3.x version).
*   **Bootstrap Framework:** Version 3.x (CSS and JavaScript components are necessary for modals, grid styling, and overall layout).
*   **Bootstrap SelectPicker:** (e.g., `bootstrap-select.js`) A plugin for enhancing HTML select elements with Bootstrap styling and features like search and multiselect.
*   **Bootstrap DateTimePicker:** (e.g., Eonasdan's Bootstrap 3 DateTimePicker - `bootstrap-datetimepicker.js` and associated CSS) For user-friendly date and time selection.
*   **CKEditor:** The rich text editor used for properties annotated for HTML or multiline text input. Ensure the necessary CKEditor scripts are included in your project.
*   **jQuery Validate:** (e.g., `jquery.validate.js`, `jquery.validate.unobtrusive.js`) For client-side form validation.
*   **jQuery Unobtrusive AJAX:** (`jquery.unobtrusive-ajax.js`) Used for the AJAX form submissions in modals.

## Key Features

These scaffolding templates offer a comprehensive set of features to accelerate your web development:

*   **Automated CRUD Scaffolding:** Generates fully functional ASP.NET MVC Controllers and Razor Views for Create, Read, Update, and Delete operations based on your Entity Framework models.
*   **AJAX-Driven Dynamic Grid:** Provides a responsive and interactive data grid:
    *   **Server-Side Searching/Filtering:** Efficiently search and filter data directly on the server.
    *   **Server-Side Sorting:** Perform data sorting on the server, reducing client-side load.
    *   **Server-Side Paging:** Handle large datasets with server-side pagination for optimal performance.
*   **Modal-Based UI:** Implements Create, Edit, Details, and Delete operations using Bootstrap modals, offering a smoother user experience by avoiding full page reloads.
*   **Bulk Deletion:** Allows users to select and delete multiple records directly from the grid.
*   **Data Export:** Supports exporting data from the grid to:
    *   Excel format
    *   CSV format
    *   Options to export either the current page data or all data.
*   **Related Entities Support:** Automatically generates dropdown lists for related entities (foreign keys), utilizing the Bootstrap SelectPicker plugin for an enhanced user interface.
*   **Rich Text Editing:** Integrates CKEditor for properties marked with `[DataType(DataType.Html)]` or `[DataType(DataType.MultilineText)]` and `[UIHint("Html")]`, enabling rich text input.
*   **Comprehensive Validation:**
    *   **Client-Side Validation:** Leverages jQuery Validate for immediate feedback in the browser.
    *   **Server-Side Validation:** Ensures data integrity through robust server-side checks.
*   **Generic Repository Pattern:** Built upon a flexible Generic Repository Pattern for data access, promoting maintainable and testable code.
*   **Asynchronous Controller Actions:** Provides an option to generate asynchronous controller actions (`async`/`await`) for improved application responsiveness and scalability.

## Installation and Setup

Follow these steps to integrate the T4 templates and associated components into your ASP.NET MVC project:

**1. T4 Template Installation:**

The core of this package is the set of T4 templates that Visual Studio uses for scaffolding.

*   **Locate Template Files:** You will find two main folders containing the T4 templates:
    *   `MvcControllerWithContext`: Contains templates for generating MVC Controllers.
    *   `MvcView`: Contains templates for generating Razor Views (Create, Edit, Delete, Details, Index).
*   **Copy to Visual Studio Directory:** You need to place these folders into your Visual Studio's scaffolding templates directory. The exact path depends on your Visual Studio version.
    *   **For Visual Studio 2015 (Version 14.0):**
        `C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Web\Mvc\Scaffolding\Templates\`
    *   **For other Visual Studio Versions (e.g., VS 2017, VS 2019, VS 2022):**
        The path will be similar. Look for `Microsoft Visual Studio XX.0` where `XX.0` is your version number (e.g., 15.0, 16.0, 17.0). You might also find them under your user's AppData folder for newer VS versions if installed per-user (e.g., `%LocalAppData%\Microsoft\VisualStudio\XX.0_XXXXXXXX\Extensions\[random_string]\Scaffolding\Templates`).
        *It's recommended to back up the original Visual Studio templates before copying the new ones.*
*   **Restart Visual Studio:** After copying the templates, restart Visual Studio for the changes to take effect.

**2. `crud-modal.js` Setup:**

This JavaScript file contains the client-side logic for handling AJAX calls, modal interactions, and dynamic grid updates.

*   **Placement:** Copy the `crud-modal.js` file into your web project, typically within the `/Scripts/` folder (e.g., `/Scripts/crud-modal.js`).
*   **Inclusion in Your Project:**
    *   **Option 1: Bundling (Recommended)**
        If you are using ASP.NET MVC's bundling and minification, add `crud-modal.js` to a relevant script bundle in your `App_Start/BundleConfig.cs` file. Make sure it's loaded after jQuery and Bootstrap.
        ```csharp
        // Example:
        bundles.Add(new ScriptBundle("~/bundles/customcrud").Include(
                    "~/Scripts/crud-modal.js"));
        ```
        Then, render this bundle in your main layout file (e.g., `_Layout.cshtml`), usually at the bottom of the `<body>` tag:
        ```html
        @Scripts.Render("~/bundles/jquery")
        @Scripts.Render("~/bundles/bootstrap")
        @Scripts.Render("~/bundles/customcrud") // Add your custom bundle
        @RenderSection("scripts", required: false)
        </body>
        ```
    *   **Option 2: Direct Script Tag**
        Alternatively, you can include it directly in your main layout file (`_Layout.cshtml`) using a `<script>` tag. Ensure it is placed *after* jQuery and Bootstrap are loaded:
        ```html
        <script src="~/Scripts/jquery-x.x.x.js"></script>
        <script src="~/Scripts/bootstrap.js"></script>
        <script src="~/Scripts/crud-modal.js"></script>
        @RenderSection("scripts", required: false)
        </body>
        ```

**3. Client-Side Dependencies Installation:**

Ensure all client-side libraries listed in the "Prerequisites/Dependencies" section are installed and referenced in your project.

*   **NuGet Package Manager:** The easiest way to install most of these libraries is via the NuGet Package Manager in Visual Studio. Search for and install packages like:
    *   `jQuery`
    *   `bootstrap` (ensure it's version 3.x for compatibility with the default template styling)
    *   `bootstrap-select` (for Bootstrap SelectPicker)
    *   `Eonasdan.Bootstrap.Datetimepicker` (for Bootstrap DateTimePicker)
    *   `CKEditor` (various packages available, choose one that suits your needs or download from the official site)
    *   `jQuery.Validation`
    *   `Microsoft.jQuery.Unobtrusive.Ajax`
*   **Bundling/Referencing:** After installation, make sure these libraries are correctly bundled in your `BundleConfig.cs` (as shown above for `crud-modal.js`) or directly referenced in your layout/view files. The order of inclusion matters for some libraries (e.g., jQuery first, then Bootstrap).

**4. Server-Side Dependencies:**

As mentioned in the "Prerequisites/Dependencies" and "Overview" sections:

*   **Project References:** Your ASP.NET MVC project *must* have references to the projects or assemblies that contain the server-side components these T4 templates rely on. This primarily includes:
    *   The Data Access Layer (DAL) providing `IEntityService<T>` and its implementation (`EntityService<T>`).
    *   The `SCMS.ViewModels` (or equivalent) assembly providing `PagedList<T>`.
    *   The `SCMS.DataExport` and `SCMS.Actions` (or equivalent) assemblies for data export functionalities.
*   **Namespace Configuration:** The T4 templates often have hardcoded `using` statements (e.g., `using DAL.Repository.Persistence;`, `using SCMS.ViewModels;`). If your namespaces differ, you will need to modify the T4 templates (`.tt` files) themselves to reflect your project's structure. See the "Customization Notes" section for more details on modifying templates.

Once these setup steps are completed, you should be able to use the custom scaffolding by right-clicking on your `Controllers` folder in Visual Studio, selecting "Add" -> "New Scaffolded Item...", and then choosing "MVC 5 Controller with views, using Entity Framework" (or a similarly named option that will appear if the templates are correctly installed).

## How to Use

After completing the "Installation and Setup" steps, you can generate CRUD interfaces using the custom T4 templates.

**1. Accessing the Scaffolder:**

*   In Visual Studio, open your ASP.NET MVC project.
*   In the Solution Explorer, right-click on the `Controllers` folder (or a subfolder within it where you want to add the new controller).
*   Select **Add** -> **New Scaffolded Item...**.
*   In the "Add Scaffold" dialog, select **"MVC 5 Controller with views, using Entity Framework"** from the list of available scaffolders. Click "Add".
    *   *(Note: The name of the custom scaffolder might appear directly in this list if Visual Studio recognizes the custom templates distinctly, e.g., "MVC 5 Controller with views, using Entity Framework (CRUD AJAX Modals)". If so, select that.)*

**2. Configuring the Scaffolder:**

The "Add Controller" dialog will appear, where you need to specify the following:

*   **Model class:** Choose the Entity Framework model class for which you want to generate the CRUD interface (e.g., `Product`, `Customer`).
*   **Data context class:** Select your project's Entity Framework DbContext class (e.g., `SCMSContext`, `ApplicationDbContext`).
*   **Controller name:** Enter a name for your new controller (e.g., `ProductsController`).
*   **Views and layout pages options:**
    *   Ensure "Generate views" is checked.
    *   You can typically leave "Use a layout page" checked and specify your main layout file (e.g., `~/Views/Shared/_Layout.cshtml`).

**3. Automatic Custom Template Selection:**

*   If you have correctly placed the custom T4 template folders (`MvcControllerWithContext`, `MvcView`) into the Visual Studio scaffolding templates directory as described in the "Installation and Setup" section, the scaffolding process will **automatically** use these custom templates.
*   You do not need to manually select individual `.t4` files during the scaffolding dialog. The standard "MVC 5 Controller with views, using Entity Framework" scaffolder will pick up your custom templates by convention if they are present in the expected locations (`Templates\MvcControllerWithContext` and `Templates\MvcView`).

**4. Generated Output:**

Once you click "Add" in the "Add Controller" dialog, Visual Studio will run the T4 templates to generate the code. You should expect the following:

*   **New Controller File:** A new C# controller file (e.g., `ProductsController.cs`) will be added to your `Controllers` folder. This controller will contain actions for listing, creating, editing, deleting, and viewing details, all designed to work with the AJAX modals and data grid. If you selected the asynchronous option during template setup (if available), these actions will be `async`.
*   **Associated View Files:** A new folder named after your controller (e.g., `Views/Products`) will be created in the `Views` directory. This folder will contain Razor view files (`.cshtml`) for:
    *   `Index.cshtml`: The main view displaying the AJAX-powered data grid.
    *   `_Create.cshtml`: The partial view for the "Create" modal form.
    *   `_Edit.cshtml`: The partial view for the "Edit" modal form.
    *   `_Delete.cshtml`: The partial view for the "Delete" confirmation modal.
    *   `_Details.cshtml`: The partial view for the "Details" modal.
    *   (And potentially other partials used by the grid or modals).
*   **Rich Functionality:** These generated files will be pre-configured with the features described earlier, including the AJAX grid with server-side operations, modal forms for CRUD actions, support for related entities, data export, and validation.

You can then navigate to the `Index` action of your new controller in a web browser (e.g., `/Products`) to see the generated CRUD interface in action. Remember to build your project first.

## Customization Notes

While the T4 templates provide a feature-rich starting point, you may want to customize various aspects of the generated code or behavior.

**1. Modifying T4 Templates:**

For deeper customization of the generated output, you can directly edit the T4 template files (`.t4` and associated `.tt` files).

*   **Location:** These files are located in the `MvcControllerWithContext` and `MvcView` folders that you copied to your Visual Studio scaffolding directory.
*   **Scope:** You can modify the C# code generated in controllers, the Razor markup in views, or the CSS classes applied to elements. This gives you fine-grained control over the scaffolded output.
*   **Examples:**
    *   Changing the default number of items per page in the grid.
    *   Adding custom logging or auditing calls within controller actions.
    *   Altering the HTML structure of the generated forms or grid.
    *   Integrating different client-side plugins or libraries.
*   **Caution:** Before making extensive modifications to the T4 templates, it's highly recommended to back up the original versions. This will allow you to revert if needed or compare changes. Editing T4 templates requires some understanding of their syntax and how they interact with the Visual Studio scaffolding process.

**2. `crud-modal.js` Behavior:**

The `crud-modal.js` file (typically found in your project's `/Scripts/` folder after setup) is central to the client-side functionality of the generated CRUD interface.

*   **Responsibilities:** This script handles:
    *   AJAX calls for loading data into the grid (search, sort, page).
    *   Displaying and hiding Bootstrap modals for Create, Edit, Delete, and Details operations.
    *   Submitting form data via AJAX from the modals.
    *   Initializing client-side plugins like Bootstrap SelectPicker, Bootstrap DateTimePicker, and CKEditor on dynamically loaded content.
    *   Client-side validation feedback and error handling for AJAX operations.
*   **Customization:** If you need to alter these client-side behaviors—such as changing modal animation effects, modifying AJAX request/response handling, adjusting options for the integrated plugins (e.g., date formats for DateTimePicker, toolbar for CKEditor), or implementing custom JavaScript logic before/after modal operations—this is the primary file to investigate and modify.

**3. Styling and CSS:**

The visual appearance of the generated views is primarily based on Bootstrap 3.x conventions.

*   **Bootstrap Dependency:** The T4 templates generate HTML markup with standard Bootstrap classes for layout, grids, forms, modals, buttons, etc.
*   **Custom Styling:** To customize the look and feel:
    *   **Override Bootstrap:** You can override default Bootstrap styles by adding your own CSS rules in your project's custom stylesheets (e.g., `Content/Site.css`). Ensure your custom stylesheet is loaded after the Bootstrap CSS.
    *   **Custom Classes:** The T4 view templates can also be modified to include custom CSS classes, allowing for more targeted styling.
    *   **Bootstrap Themes:** For a more significant visual change, consider using a different Bootstrap theme.

By understanding these customization points, you can tailor the generated CRUD interfaces to better fit your application's specific requirements and design.

## Project Structure Expectation

This section outlines the assumptions made by the T4 templates regarding your project's structure, class names, and namespaces. Understanding these expectations can help you determine if the templates are a direct fit or what adjustments might be needed.

**1. Assumed Dependencies & Namespaces:**

The T4 templates are written with the expectation that certain classes, interfaces, and namespaces are available within your target ASP.NET MVC project. The generated code will rely on these components. Key dependencies include:

*   **Data Access Layer (DAL):**
    *   Interface: `DAL.Repository.Persistence.IEntityService<T>`
    *   Implementation: `DAL.Repository.Persistence.EntityService<T>`
    *   *(These are used for generic repository operations within the generated controller.)*
*   **Database Context (Entity Framework):**
    *   The templates often refer to a DbContext named `SCMSContext` (e.g., `private SCMSContext db = new SCMSContext();`).
    *   If your project's DbContext is named differently (e.g., `ApplicationDbContext`, `MyProjectContext`), you will need to update this in the controller T4 template (`MvcControllerWithContext\Controller.cs.t4`) and potentially in the `ControllerWithRepository.cs.t4` if you use that variant.
*   **View Models:**
    *   `SCMS.ViewModels.PagedList<T>`: This class is expected for handling pagination logic in the `Index` action and view.
*   **Utility Classes (for Data Export):**
    *   `SCMS.DataExport.ExcelFormatter`: Used by the controller to format data for Excel export.
    *   `SCMS.DataExport.CsvResult`: A custom `ActionResult` for returning CSV files.
    *   `SCMS.Actions.ExcelResult`: A custom `ActionResult` for returning Excel files.

**2. Adaptability & Required Modifications:**

If your project's structure, class names, or namespaces differ from those listed above, you will likely need to modify the T4 templates to align with your setup. The most common place for these changes is within the controller template files (e.g., `MvcControllerWithContext\Controller.cs.t4`).

*   **Key Areas for Modification in T4 Templates:**
    *   **`using` Statements:** Adjust the `using` statements at the top of the template to import your project's specific namespaces.
    *   **Variable Declarations:** Update declarations and instantiations of the DbContext and any service layer components to match your class names and dependency injection patterns if applicable. For instance, how the `IEntityService<T>` is instantiated or injected into the controller.
    *   **Method Calls:** If your service or utility classes have different method signatures, these will also need to be updated in the template.

**3. Purpose of this Information:**

Providing these details on project structure expectations aims to help you:

*   Quickly assess if these T4 templates are a good out-of-the-box fit for your existing project.
*   Understand the potential modifications required to integrate the templates successfully if your project has a different architecture or naming conventions.
*   Streamline the setup process by highlighting common areas that might need adjustment.

By anticipating these dependencies, you can more effectively leverage or adapt these T4 scaffolding templates for your development needs.

## License

This project, including the T4 templates and associated `crud-modal.js` script, is licensed under the MIT License. You are free to use, modify, and distribute this software in accordance with the terms of the license.

For the full license text, please see the [LICENSE](LICENSE) file located in the root of this repository.
