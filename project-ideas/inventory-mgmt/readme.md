Inventory Management systems 

[Inventory data model](Inventory.md)

InventoryItem
InventoryItemStatus
InventoryItemDetail
InventoryItemVariance
PhysicalInventory
PhysicalInventoryAndVariance
InventoryTransfer

getMktgPackagesAvailable
issueImmediatelyFulfilledOrder
issueImmediatelyFulfilledOrderItem,

### Inventory Reservation Cancellation Services in OFBiz

Here's a breakdown of the three services related to canceling inventory reservations in OFBiz, along with their descriptions and parameters:

1.  **`cancelOrderInventoryReservation`**

    *   **Description:** This service cancels all inventory reservations associated with a specific order. It iterates through the order's items and calls other services to handle cancellations at a more granular level.
    *   **Input Parameters:**
        *   `orderId` (required): The ID of the order for which to cancel inventory reservations.
        *   `orderItemSeqId` (optional): The sequence ID of a specific order item to cancel reservations for. If not provided, reservations for all order items within the order will be canceled.
        *   `shipGroupSeqId` (optional): The sequence ID of a specific shipment group to cancel reservations for. If not provided, reservations for all shipment groups within the order will be canceled.
    *   **Output Parameters:**
        *   The service doesn't explicitly define output parameters in the XML definition. However, like most OFBiz services, it likely returns a `Map` with a `success` boolean field and an optional `errorMessage` field.

2.  **`cancelOrderItemInvResQty`**

    *   **Description:** This service cancels a specific quantity of a reserved inventory item for a given order item.
    *   **Input Parameters:**
        *   `orderId` (required): The ID of the order.
        *   `orderItemSeqId` (required): The sequence ID of the order item.
        *   `shipGroupSeqId` (optional): The sequence ID of the shipment group. If not provided, it might cancel the quantity from any reservation associated with the order item.
        *   `cancelQuantity` (optional): The quantity of the reservation to cancel. If not provided, the entire reservation might be canceled.
    *   **Output Parameters:**
        *   Similar to the previous service, it likely returns a standard `Map` indicating success or failure.

3.  **`cancelOrderItemShipGrpInvRes`**

    *   **Description:** This service cancels an entire inventory reservation for a specific order item, shipment group, and inventory item combination.
    *   **Input Parameters:**
        *   `orderId` (required): The ID of the order.
        *   `orderItemSeqId` (required): The sequence ID of the order item.
        *   `shipGroupSeqId` (required): The sequence ID of the shipment group.
        *   `inventoryItemId` (required): The ID of the `InventoryItem` for which to cancel the reservation.
        *   `cancelQuantity` (optional): The quantity of the reservation to cancel. If not provided, the entire reservation is canceled.
    *   **Output Parameters:**
        *   It likely returns a standard `Map` indicating success or failure.

**Important Notes:**


## Rejection:
1. Single ATP reduced by rejection
2. Single ATP and QoH reduced by rejection
3. Both of the above but for all qty
4. Release reservation and increase ATP
Link Order and Item to event

## Cycle Count:
1. Variance QoH to match counted Qty
2. Variance ATP to match counted Qty - Reservations
Link count and count item to event

## Log variance:
1. Log variance on ATP and QoH by given amount with given reason
Link userLogin to event

## Item shipped:
1. Reduce ATP for reservation
2. Reduce QoH for item shipped
Link order,, order item, shipment and shipment item to both events

## POS Sale:
1. Reduce ATP and QoH for item sold in store
Link order and item to event

##  Increase ATP and QoH
Link order, order item, shipment and shipment item to event

