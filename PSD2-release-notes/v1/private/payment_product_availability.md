## Payment Type Availability — Private PSD2 Payment Initiation API
During the migration, payment types are moved incrementally from the legacy (v8) PSD2 Payment Initiation API to the new Private API (v1). The table below shows current environment availability per payment type.
For each payment type, availability in production in the new API means that the same payment type in the legacy PSD2 Payment Initiation API enters its deprecation phase.

| Payment Type                           | Payment Type ID (v8)                            | PSD2 Payment Initiation (v8)       | Payment Type ID (v1)                       | Private PSD2 Payment Initiation (v1) |
|----------------------------------------|-------------------------------------------------|------------------------------------|--------------------------------------------|--------------------------------------|
| Swedish domestic credit transfer       | swedish-domestic-private-credit-transfers       | Production (Deprecated 2026-08-28) | private-se-domestic-credit-transfers       | Production                           |
| Transfers between own Swedish accounts | swedish-domestic-private-own-accounts-transfers | Production (Deprecated 2026-08-28) | private-se-domestic-own-credit-transfers   | Production                           |
| Swedish domestic Bankgiro payment      | swedish-domestic-private-bankgiros              | Production (Deprecated 2026-11-26) | private-se-domestic-alias-credit-transfers | Production                           |
| Swedish domestic PlusGiro payment      | swedish-domestic-private-plusgiros              | Production (Deprecated 2026-11-26) | private-se-domestic-alias-credit-transfers | Production                           |
| SEPA credit transfer                   | sepa-credit-transfers                           | Production (Deprecated 2026-11-26) | private-sepa-credit-transfers              | Production                           |
| Cross-border credit transfer           | cross-border-credit-transfers                   | Production                         | TBA                                        | TBA                                  |
