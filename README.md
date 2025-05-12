# DES3D Configuration Web Form Generator

This repository hosts a web-based form designed to help users generate configuration files for the DES3D simulation program. The parameters in this form are derived from the `boost::program_options` definitions found in the DES3D C++ source code (specifically, the `declare_parameters()` function in an `input.cxx` file).

The goal of this tool is to provide a user-friendly interface for setting up simulation parameters and to output a configuration file (e.g., `.cfg`, `.ini` format) that can be directly used by the DES3D application.

## Features

* **Dynamic Form Generation:** The web form lists all known DES3D parameters, grouped by sections (e.g., `[sim]`, `[mesh]`, `[control]`, etc.).
* **Parameter Descriptions:** Each parameter includes its detailed description as found in the C++ source code.
* **Default Values:** Default values (where specified in the C++ source) are pre-filled in the form.
* **Type-Aware Inputs:** Uses appropriate HTML input types (text fields, number inputs, dropdowns for booleans and enumerated choices).
* **Collapsible Sections:** Each parameter group can be conveniently folded and unfolded for easier navigation of the form.
* **Upload User Configuration:** Allows users to upload their own existing DES3D configuration files (e.g., `.cfg`, `.ini`). The form fields are then pre-filled with the values from the uploaded file. Parameters loaded this way are visually highlighted (e.g., in blue text) to distinguish them from default values.
* **Load GitHub Examples:** Fetches and lists available example `.cfg` files directly from the `GeoFLAC/DynEarthSol/tree/master/examples` GitHub repository. Users can select an example from a dropdown to pre-fill the form, providing quick access to standard or test setups. Parameters loaded from examples are also visually highlighted.
* **Generate Config Output:** Displays the generated configuration text in the `boost::program_options` compatible INI-style format (`[section]\nparameter_short_name = value`).
* **Download Config File:** Allows users to download the generated configuration, typically as a `.cfg` file, using the `sim.modelname` for the filename if provided.

## Usage

1.  **Access the Web Form:**
    * **Online (GitHub Pages):** This tool is hosted on GitHub Pages at: [https://geoflac.github.io/des-inputgen/](https://geoflac.github.io/des-inputgen/)
        *(Ensure this URL is correct based on your GitHub Pages setup for this repository).*
    * **Locally:** Download or clone this repository. Open the `index.html` file in your web browser.

2.  **Using the Form:**
    * **Starting Fresh:** Navigate through the collapsible sections and manually input your desired values for each parameter. Descriptions are provided for guidance.
    * **Uploading Your Config:**
        * Click on the "Upload Existing Config File" input field.
        * Select your local `.cfg` or `.ini` file.
        * The form fields will automatically update with values from your file. Values loaded from your file will appear in blue text. Other fields will retain their default values (in black text). An informational message will confirm the file processing.
    * **Loading an Example from GitHub:**
        * The dropdown list under "Load Example Config from GitHub" will populate with available `.cfg` files from the `GeoFLAC/DynEarthSol` examples directory.
        * Select an example file from the list.
        * Click the "Load Example" button.
        * The form fields will update with values from the selected example. Values loaded from the example will appear in blue text.
    * **Generate:** Once the form is populated (either manually, by upload, or from an example), click the "Generate Config" button. The formatted configuration text will appear in the text area below. Any required fields that are empty will be flagged.
    * **Download:** If the configuration is generated successfully, click the "Download Config File" button to save it.

## Structure of the Repository (Primary Files)

* `index.html`: The main web page containing the form, embedded CSS, and JavaScript logic.
* `parameters.js`: The JavaScript file containing the `parameters` array, loaded by `index.html`.
* `README.md`: This file.

## Development / Contributing

(You can add details here if you want others to contribute or if you have specific setup instructions for development)

* To update the parameter list, obtain the latest `input.cxx` from the DES3D project.
* The main form logic and UI are within `index.html`.

## Future Enhancements (Ideas)

* Automating the parameter synchronization (`input.cxx` -> Web Form)
   * The parameters in the web form are defined in a JavaScript array, `parameters.js` file.
   * To keep this synchronized with the `input.cxx` file from the main DES3D source code, one needs to read the changes to `input.cxx` and add them to `parameters.js`.
* More sophisticated UI for list-based parameters (e.g., materials, fault segments) if applicable.
* Advanced validation based on parameter interdependencies or ranges.
* Visual themes or styling improvements.

---
*This README was last updated on May 12, 2025.*
