👜 Evidence Bags Script

A QBCore & ESX compatible script for handling seized evidence.
Officers can bag, seal, and present items in evidence bags for realistic roleplay.

📂 Folder Structure
evidencebags/
│── fxmanifest.lua
│── config.lua
│── server.lua
│── client.lua
│
├── qb/
│   └── items.lua       # For qb-core/shared/items.lua
│
├── esx/
│   └── items.sql       # For ESX database
│
└── README.md

⚙️ Features

👮 Police can bag any item from a suspect.

📦 Multiple items per bag (configurable, default = 5).

🔒 Seal/Unseal system:

Police can seal bags.

Police/Judges can unseal bags.

Civilians can only inspect.

🖱️ Third Eye + Commands (works with qb-target/ox_target and /bagitem, /sealbag, /unsealbag).

📑 Metadata stored:

Bag ID

Officer name & ID

Suspect name & ID

Date seized

Sealed status

Item list

📋 Commands
Command	Usage	Description
/bagitem [id] [item] [amount]	/bagitem 3 weed_bag 2	Bags 2 weed bags from ID 3 into evidence bag.
/sealbag	/sealbag	Seals the officer’s evidence bag (cannot add more items).
/unsealbag	/unsealbag	Unseals bag (Police/Judge only).
/inspectbag	/inspectbag	Shows full bag details and contents.
📦 Items
QBCore (add to qb-core/shared/items.lua):
['evidence_bag'] = {
    ['name'] = 'evidence_bag',
    ['label'] = 'Evidence Bag',
    ['weight'] = 100,
    ['type'] = 'item',
    ['image'] = 'evidence_bag.png',
    ['unique'] = true,
    ['useable'] = true,
    ['shouldClose'] = true,
    ['combinable'] = nil,
    ['description'] = 'A sealed bag containing seized evidence.'
},

ESX (run in DB):
INSERT INTO items (name, label, weight) VALUES
('evidence_bag', 'Evidence Bag', 1);

🔧 Config

Located in config.lua:

Config = {}

-- Framework: "qbcore" or "esx"
Config.Framework = "qbcore"

-- Evidence bag item
Config.EvidenceItem = "evidence_bag"

-- Max items per bag
Config.MaxEvidenceItems = 5

🔄 Workflow Example

Police officer finds drugs on a suspect.

Uses /bagitem 4 weed_bag 5 to confiscate and bag them.

If they already have an unsealed bag, items are added.

If not, a new bag is created.

Officer seals the bag with /sealbag.

Later in court, the Judge inspects the bag with /inspectbag.

If necessary, Judge/Police can /unsealbag to return the evidence items.

⚖️ Notes

Evidence bags are unique items with metadata (ID, officer, suspect, items, etc).

Civilians can never alter bags — only inspect them.

Supports both QBCore and ESX out of the box.

Any item can be bagged (weapons, drugs, cash, random items).
