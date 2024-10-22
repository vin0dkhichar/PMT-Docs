# G2P: Proxy Means Test

PMT is a module used within the OpenG2P to effectively identify and manage social welfare beneficiaries. By employing proxy means test, it utilizes observable individual and household characteristics-such as assets, education, and living conditions-to estimate economic status, circumventing the limitations of self-reported income. This approach enhances the precision of targeting by ensuring that benefits are directed to those who truly need them while minimizing errors of inclusion and exclusion. With its robust design, it integrates seamlessly into systems, improving the overall efficiency.

## Feature and functionality

| **PMT method** | **PMT process**  |
| ------- | --- |
| **PMT Calculation** | <ul><li>The module supports Proxy Means Test by calculating a score for each registrant based on various parameters. </li><li>Fields related to PMT are computed and stored, which can be referenced later for decision-making.</li></ul>|
| **Proxy Means Test Parameters** | The `ProxyMeanTestParams` class manages proxy means test parameters, including selecting fields from registrant information to use in calculating PMT scores and assigning weightage to those fields for scoring purposes. |
| **Dynamic Field Weightage for PMT** | <ul><li>The PMT parameters (fields and their weightages) are customizable. For Individual and Group, an administrator can define which fields will be included in the PMT score calculation and assign specific weightages to each field.</li><li>This is handled by selecting fields dynamically chosen based on their types (`integer` or `float`).</li></ul>|
| **Managing Fields Deletion** | The `IrModelFields.unlink` method ensures that when a field related to a PMT parameter is deleted from the model, the system also deletes the corresponding PMT records. This maintains data integrity and ensures that PMT configurations are not left in an inconsistent state. |

## Salient Design Features
1. **Model Inheritance:**
   - The module heavily relies on model inheritance, allowing it to extend functionality for existing Odoo models.
   - This ensures that the existing behavior of these models is preserved while adding custom PMT-specific functionality.

2. **Dynamic Field Selection:**
   - The selection of fields for PMT is dynamic and based on introspection of the model, ensuring that only relevant fields (integers or floats) can be used in PMT calculations. This guards against errors where non-numeric fields (e.g., strings or dates) might otherwise be selected.

4. **Computations and Dependencies:**
   - The PMT score is computed dynamically using Odoo's `@api.depends` decorator, ensuring that the score is recalculated whenever relevant fields are modified.
5. **Field Deletion Handling:**
   - The design ensures that when a field used in PMT is deleted from the `ir.model.fields`, it is also removed from the PMT configuration. This avoids orphaned records in the table.

## Source Code

## Related User Guides
[PMT](https://docs.openg2p.org/pbms/functionality/eligibility/proxy-means-test)
