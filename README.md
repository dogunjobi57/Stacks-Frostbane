
### Stacks-Frostbane -  Game Items Smart Contract

This Clarity smart contract manages in-game item creation, transfer, character progression, and marketplace listing on the Stacks blockchain. Designed with efficiency and scalability in mind, it includes both batch and single-item operations with access control and validation logic.

---

### 📦 **Features**

* ✅ **Item Creation**

  * Single or batch item creation by the platform admin.
* 🔄 **Item Transfer**

  * Players can transfer items they own to other players.
  * Batch transfers supported.
* 🛒 **Marketplace Listing**

  * Players can list items for sale.
  * Includes price and timestamp metadata.
* 📈 **Character Progression**

  * Read-only tracking of character experience and level.
* 🔍 **Data Access**

  * Read-only views for item details, marketplace listings, and character progression.

---

### 🛠️ **Contract Structure**

#### Constants

| Constant                   | Description                                        |
| -------------------------- | -------------------------------------------------- |
| `platform-admin`           | The admin (usually contract deployer or tx-sender) |
| `max-character-level`      | Cap on character level (100)                       |
| `max-character-experience` | Cap on experience points (10,000)                  |
| `max-item-metadata-length` | Max URI length for metadata (256)                  |
| `max-batch-operation-size` | Max items in batch operations (10)                 |

---

### 🧩 **Data Variables**

* `total-item-count` – Tracks number of created items.

---

### 🗺️ **Maps**

| Map                         | Purpose                                  |
| --------------------------- | ---------------------------------------- |
| `game-items`                | Stores item data by ID                   |
| `item-market-values`        | (Reserved for future use: item pricing)  |
| `character-progression`     | Maps characters to their XP and level    |
| `marketplace-item-listings` | Active listings with price & seller info |

---

### 🔐 **Access Control**

* Only the **platform admin** can:

  * Create items (`create-item`, `batch-create-items`)

---

### ✅ **Public Functions**

| Function               | Description                        |
| ---------------------- | ---------------------------------- |
| `create-item`          | Admin-only: Create a new item      |
| `batch-create-items`   | Admin-only: Create multiple items  |
| `transfer-item`        | Player transfers an item they own  |
| `batch-transfer-items` | Transfer multiple items            |
| `list-item-for-sale`   | List owned item on the marketplace |

---

### 👁️ **Read-Only Functions**

| Function                    | Description               |
| --------------------------- | ------------------------- |
| `get-item-details`          | View metadata of an item  |
| `get-marketplace-listing`   | View listing details      |
| `get-character-progression` | View character XP & level |
| `get-total-items`           | Total created items       |

---

### ⚠️ **Errors**

| Code                              | Meaning                            |
| --------------------------------- | ---------------------------------- |
| `err-admin-only` (`u100`)         | Only the admin can call this       |
| `err-resource-not-found` (`u101`) | Item not found                     |
| `err-permission-denied` (`u102`)  | Invalid transfer or listing        |
| `err-invalid-parameters` (`u103`) | Bad input (e.g., mismatched lists) |
| `err-pricing-error` (`u104`)      | Pricing rules not met              |

---

### 🔄 **Example Flow**

1. Admin calls `create-item` or `batch-create-items`.
2. Players receive items via `transfer-item` or batch.
3. Players list items with `list-item-for-sale`.
4. Buyers query listings with `get-marketplace-listing`.

---
