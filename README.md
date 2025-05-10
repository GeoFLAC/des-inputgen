# des-inputgen: DES3D Configuration Web Form Generator

This repository contains a web-based form to help users generate configuration files for the DES3D simulation program. The parameters in this form are derived from the `boost::program_options` definitions found in the DES3D C++ source code (specifically, the `declare_parameters()` function in `input.cxx`).

The goal of this tool is to provide a user-friendly interface for setting up simulation parameters and to output a configuration file (`.cfg` or `.ini` format) that can be directly used by the DES3D application.

## Features

* **Dynamic Form Generation:** The web form lists parameters grouped by sections (e.g., `[sim]`, `[mesh]`, `[control]`, etc.).
* **Parameter Descriptions:** Each parameter includes its description as found in the C++ source code.
* **Default Values:** Default values (where specified in the C++ source) are pre-filled.
* **Type-Aware Inputs:** Uses appropriate HTML input types (text, number, select for booleans/enums).
* **Collapsible Sections:** Each parameter group can be folded and unfolded for better navigation.
* **Upload Existing Config:** Users can upload an existing DES3D configuration file to pre-fill the form.
* **Generate Config Output:** Displays the generated configuration text in the `boost::program_options` format.
* **Download Config File:** Allows users to download the generated configuration as a `.cfg` file.

## How It Works

The primary component is a static `index.html` page that uses JavaScript to:
1.  Define a comprehensive list of all DES3D parameters (names, types, descriptions, defaults). This list is ideally generated/updated by the `parse_parameters.py` Python script included in this repository (or to be included).
2.  Dynamically render the HTML form elements based on these parameter definitions.
3.  Handle user input and selections.
4.  Parse uploaded configuration files to update form fields.
5.  Generate the output configuration string in the format:
    ```ini
    [section_name]
    parameter_short_name = value
    ```

## Usage

1.  **Access the Web Form:**
    * **Online (GitHub Pages):** This tool is hosted on GitHub Pages at: [https://geoflac.github.io/des-inputgen/](https://geoflac.github.io/des-inputgen/)
    * **Locally:** Download or clone this repository. Open the `index.html` file in your web browser.

2.  **Using the Form:**
    * **Fill in Parameters:** Navigate through the collapsible sections and input your desired values for each parameter. Descriptions are provided for guidance. Required parameters might be indicated.
    * **(Optional) Upload Existing Config:** Use the "Upload Existing Config File" button to select a `.cfg` or `.ini` file. The form fields will be updated with values from this file.
    * **Generate:** Click the "Generate Config" button. The formatted configuration text will appear in the text area below.
    * **Download:** Click the "Download Config File" button to save the generated configuration. The filename will typically be based on the `sim.modelname` parameter or default to `parameters.cfg`.

## Maintaining Parameter Synchronization (`input.cxx` -> Web Form)

The parameters in the web form are defined in a JavaScript array within the `index.html` file (or a linked `generated_parameters.js` file). To keep this synchronized with the `input.cxx` file from the DES3D source code:

1.  **`parse_parameters.py` Script:**
    This repository includes (or should include) a Python script named `parse_parameters.py`. This script is designed to:
    * Read the `input.cxx` file (you'll need to place a copy of the relevant `input.cxx` in the same directory as the script or provide its path).
    * Parse the `declare_parameters()` function to extract all parameter definitions.
    * Generate a JavaScript file (e.g., `generated_parameters.js`) containing the updated `parameters` array.

2.  **How to Update:**
    * Whenever `input.cxx` in the main DES3D project changes (parameters added, removed, or modified):
        1.  Copy the latest `input.cxx` to the directory containing `parse_parameters.py`.
        2.  Run the Python script: `python parse_parameters.py`
        3.  This will update/create `generated_parameters.js`.
        4.  Ensure your `index.html` correctly loads this `generated_parameters.js` file.
        5.  Commit the changes to `generated_parameters.js` (and `index.html` if its script loading changed) to this repository.

    *(Note: You might need to manually review and adjust the `enum_like_options` dictionary within `parse_parameters.py` if new integer parameters are added that should be represented as dropdowns with specific choices.)*

## Structure of the Repository

* `index.html`: The main web page containing the form, CSS, and JavaScript logic.
* `(Optional) style.css`: Separate CSS file if not inlined.
* `(Optional) script.js`: Separate JavaScript file if not inlined.
* `input.cxx`: A copy of the C++ source file from which parameters are derived (for reference and for the parser script).
* `parse_parameters.py`: Python script to parse `input.cxx` and generate the JavaScript parameter definitions.
* `(Optional) generated_parameters.js`: The auto-generated JavaScript file containing the `parameters` array.
* `README.md`: This file.

## Development / Contributing

* `parameters.js` needs to be updated to reflect any new changes to `input.cxx`.
  * This process will be automated in the future.
* The form logic and UI are in `index.html` (or linked JS/CSS files).

## Future Enhancements (Ideas)

* More sophisticated UI for list parameters (e.g., lists of material properties).
* Advanced validation based on parameter interdependencies.
* Directly using a C++ parsing library in the Python script for more robust extraction from `input.cxx`.
* Visual themes or styling improvements.

---

Generated on: May 9, 2025
