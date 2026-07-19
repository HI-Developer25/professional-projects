# 🧗 Challenges & Solutions — ERP & Logistics Systems

[← Back to project overview](./README.md)

### Stock discrepancies between POS and inventory

**Challenge:** Inventory counts drifted out of sync with point-of-sale activity, creating discrepancies that affected order fulfillment accuracy.

**Solution:** Reworked the POS inventory-sync logic, cutting discrepancies by roughly 50%.

### Fragmented shipment tracking across couriers

**Challenge:** Orders shipped through different courier partners meant customers had no single, consistent way to track a shipment.

**Solution:** Integrated 4+ courier APIs into the order-fulfillment system to provide real-time tracking regardless of which courier handled a given shipment.

### Working across three different PHP frameworks

**Challenge:** ERP modules across different client systems were built on Laravel, Yii, and CodeIgniter respectively, each with its own conventions.

**Solution:** Adapted to each framework's existing patterns rather than forcing a one-size-fits-all approach, keeping changes consistent with each codebase's conventions.

---
<sub>Part of the [ERP & Logistics Systems](./README.md) case study.</sub>
