# Smart Restaurant Billing System

A clean, interactive command-line interface (CLI) billing and point-of-sale (POS) application built with standard Python. Designed for cafes, diners, and small restaurants to manage digital ordering, multi-tier discount logic, tax computation, and automated text receipt export.

---

## Key Features

- **Interactive Menu Display**: Dynamically lists catalog items numbered sequentially with local currency formatting.
- **Robust Order Management**:
  - Item selection by index.
  - Custom quantity inputs with automatic data validation.
  - Live order preview before finalizing invoices.
- **Dynamic Pricing & Discount Engine**:
  - **Customer Tier Discounts**:
    - Regular: 0%
    - Student: 5%
    - Couple: 10%
    - Premium: 15%
  - **Bulk Order Discount**: 10% off orders with subtotals exceeding Rs. 1,000.
  - **Optimal Savings Logic**: Automatically selects the larger rate between tier-based and bulk discount (non-stacking protection).
- **Tax & Total Calculations**: Applies post-discount sales tax (5% default) in accordance with standard retail accounting standards.
- **Formatted Receipts & File Export**:
  - Neatly aligned tabular layout for thermal/monospaced printing.
  - Automatically exports a timestamped copy to `receipt.txt`.
- **Zero External Dependencies**: Built entirely with Python's standard library (`datetime`).

---

## Project Structure

```text
.
├── billing.py          # Main application script
├── receipt.txt         # Auto-generated receipt file (created upon billing)
└── README.md           # Documentation
```

---

## Requirements

- Python 3.6 or higher.
- No third-party packages required (`pip install` not needed).

---

## Getting Started

### 1. Clone or Download the Repository

Save the Python script as `billing.py` in your project folder.

### 2. Run the Application

Execute the script via terminal or command prompt:

```bash
python billing.py
```

---

## Usage Workflow

1. **Main Navigation**: Choose whether to browse the menu, start an order, or exit.
   ```text
   ========================================
                  MAIN MENU                
   ========================================
   1. Place a New Order
   2. View Restaurant Menu
   3. Exit
   ========================================
   ```
2. **Taking Orders**: Select items by their numerical ID and enter quantity. Enter `0` when order selection is complete.
3. **Review Summary**: Inspect the itemized draft order.
4. **Select Customer Tier**: Choose the appropriate loyalty or customer category (e.g., Student, Premium).
5. **Bill Output**: The terminal renders the final formatted invoice and overwrites/updates `receipt.txt`.

---

## Sample Receipt Output (`receipt.txt`)

```text
========================================
          The Python Kitchen           
========================================
Date: 11-10-2026 21:45:10
----------------------------------------
Item                 Qty         Amount
----------------------------------------
Paneer Tikka           2        Rs.360
Chicken Biryani        2        Rs.520
Cold Coffee            2        Rs.180
----------------------------------------
Subtotal                 Rs.1060.00
Customer Type: Premium Customer
Discount                 -Rs.159.00
Tax                      Rs.45.05
========================================
TOTAL                    Rs.946.05
========================================
        Thank you! Visit again.         
```

---

## Configuration & Customization

All primary configurations and business rules are declared at the top of `billing.py`:

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `RESTAURANT_NAME` | `str` | `"The Python Kitchen"` | Heading displayed on menus and invoices |
| `CURRENCY_SYMBOL` | `str` | `"Rs."` | Symbol prefixed to all currency numbers |
| `TAX_RATE` | `float` | `0.05` | Sales tax rate (e.g., `0.05` for 5%) |
| `DISCOUNT_RATE` | `float` | `0.10` | Percentage discount applied on qualifying bulk orders |
| `DISCOUNT_MIN_AMOUNT`| `int` / `float` | `1000` | Minimum order subtotal required for bulk discount |
| `CUSTOMER_DISCOUNTS` | `dict` | *See settings* | Tier-based percentage rates |
| `RECEIPT_FILE_NAME` | `str` | `"receipt.txt"` | Target output filename for receipts |

### Modifying the Menu
To add, remove, or change menu item prices, update the `menu` dictionary in `billing.py`:

```python
menu = {
    "Spring Roll": 120,
    "Paneer Tikka": 180,
    "Chicken Wings": 220,
    # Add new items:
    "Garlic Bread": 110,
}
```

---

## Code Architecture

- **Data Models**: Simple dictionaries for menu definitions (`{item: price}`) and line-item dictionaries (`{"name": ..., "price": ..., "qty": ...}`).
- **Defensive Input Handling**: `get_number()` and `get_yes_no()` enforce strict type validation and looping prompts against invalid CLI input.
- **Decoupled Business Logic**: Separation of subtotal aggregation, discount comparison, and post-discount tax computation into standalone pure functions (`get_subtotal`, `get_discount`, `get_tax`, `calculate_bill`).

---

## License

This project is open-source and free to use for personal, educational, or commercial purposes.
