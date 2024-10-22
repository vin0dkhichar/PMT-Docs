# Proxy Means Test

Proxy Means Test (PMT) is a method widely used by governments and international organizations to estimate income or consumption levels of households, particularly those in low and middle-income countries. PMT is a valuable tool for effectively targeting social programs and subsidies, ensuring that limited resources are allocated to those who need them the most. PMT is based on the principle that certain household characteristics, known as proxies, correlate with income and standard of living. These proxies may include household composition, housing quality, asset ownership, access to basic services, and other observable characteristics.

## Why do we need PMT?

The need for a Proxy Means Test (PMT) arises from the challenges of accurately identifying and targeting poor households for social welfare programs. Traditional means tests, which rely on reported income, often suffer from inaccuracies due to misreporting or informal employment. PMT addresses these challenges using observable household characteristics, such as assets, education level, housing conditions, and family size, to estimate a household's economic status.

## Feature and functionality

| **PMT method** | **PMT process**  |
| ------- | --- |
| **PMT Calculation** | <ul><li>The module supports Proxy Means Testing by calculating a score for each program registrant based on various parameters (`pmt_field` and `pmt_weightage`).</li><li>Fields related to PMT (`pmt_score` and `latest_pmt_score`) are computed and stored, which can be referenced later for decision-making within the program.</li></ul>|
| **Proxy Means Test Parameters** | The `ProxyMeanTestParams` class manages proxy means test parameters, including selecting fields from registrant information to use in calculating PMT scores and assigning weightage to those fields for scoring purposes. |
| **Dynamic Field Weightage for PMT** | <ul><li>The PMT parameters (fields and their weightages) are customizable. For each program, an administrator can define which fields will be included in the PMT score calculation and assign specific weightages to each field.</li><li>This is handled by selecting fields from the `g2p.program.registrant_info model`, dynamically chosen based on their types (`integer` or `float`).</li></ul>|
| **Managing Fields Deletion** | The `IrModelFields.unlink` method ensures that when a field related to a PMT parameter is deleted from the model, the system also deletes the corresponding PMT records (`g2p.proxy_means_test_params`). This maintains data integrity and ensures that PMT configurations are not left in an inconsistent state. |
| **Wizard for Creating Programs** | The `G2PCreateProgramWizard` model simplifies program creation by allowing users to specify PMT configuration during program setup. If enabled, it also creates and links the PMT parameters for the new program.|
