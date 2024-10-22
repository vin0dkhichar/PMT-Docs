# G2P: Proxy Means Test

## g2p_proxy_means_test

`g2p_proxy_means_test` is a module used within the OpenG2P to effectively identify and manage social welfare beneficiaries. By employing proxy means testing, it utilizes observable individual and household characteristics-such as assets, education, and living conditions-to estimate economic status, circumventing the limitations of self-reported income. This approach enhances the precision of targeting by ensuring that benefits are directed to those who truly need them while minimizing errors of inclusion and exclusion. With its robust design, `g2p_proxy_means_test` integrates seamlessly into systems, improving the overall efficiency of social protection programs.

## Feature and functionality

| **PMT method** | **PMT process**  |
| ------- | --- |
| **PMT Calculation** | <ul><li>The module supports Proxy Means Testing by calculating a score for each program registrant based on various parameters (`pmt_field` and `pmt_weightage`).</li><li>Fields related to PMT (`pmt_score` and `latest_pmt_score`) are computed and stored, which can be referenced later for decision-making within the program.</li></ul>|
| **Proxy Means Test Parameters** | The `ProxyMeanTestParams` class manages proxy means test parameters, including selecting fields from registrant information to use in calculating PMT scores and assigning weightage to those fields for scoring purposes. |
| **Dynamic Field Weightage for PMT** | <ul><li>The PMT parameters (fields and their weightages) are customizable. For each program, an administrator can define which fields will be included in the PMT score calculation and assign specific weightages to each field.</li><li>This is handled by selecting fields from the `g2p.program.registrant_info model`, dynamically chosen based on their types (`integer` or `float`).</li></ul>|
| **Managing Fields Deletion** | The `IrModelFields.unlink` method ensures that when a field related to a PMT parameter is deleted from the model, the system also deletes the corresponding PMT records (`g2p.proxy_means_test_params`). This maintains data integrity and ensures that PMT configurations are not left in an inconsistent state. |
| **Wizard for Creating Programs** | The `G2PCreateProgramWizard` model simplifies program creation by allowing users to specify PMT configuration during program setup. If enabled, it also creates and links the PMT parameters for the new program.|

## Salient Design Features
1. **Model Inheritance:**
   - The module heavily relies on model inheritance (`_inherit`), allowing it to extend functionality for existing Odoo models such as `ir.model.fields`, `g2p.program`, `g2p.program.registrant_info`, and the wizard (`g2p.program.create.wizard`).
   - This ensures that the existing behavior of these models is preserved while adding custom PMT-specific functionality.

2. **Dynamic Field Selection:**
   - The selection of fields for PMT is dynamic and based on introspection of the `g2p.program.registrant_info` model, ensuring that only relevant fields (integers or floats) can be used in PMT calculations. This guards against errors where non-numeric fields (e.g., strings or dates) might otherwise be selected.

4. **Computations and Dependencies:**
   - The PMT score is computed dynamically using Odoo's `@api.depends` decorator, ensuring that the score is recalculated whenever relevant fields are modified.
   - Additionally, the `latest_registrant_info` field keeps track of the most recent registration information, aiding in analysis and decision-making based on historical data.
5. **Field Deletion Handling:**
   - The design ensures that when a field used in PMT is deleted from the `ir.model.fields`, it is also removed from the PMT configuration. This avoids orphaned records in the `g2p.proxy_means_test_params` table.

## Source Code
[https://github.com/OpenG2P/openg2p-program/tree/17.0-develop/g2p_proxy_means_test](https://github.com/OpenG2P/openg2p-program/tree/17.0-develop/g2p_proxy_means_test)

## Related User Guides
[PMT](https://docs.openg2p.org/pbms/functionality/eligibility/proxy-means-test), [Configure Proxy Means Test](https://docs.openg2p.org/pbms/functionality/eligibility/user-guides/configure-proxy-means-test)
