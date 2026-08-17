## Payment Type Availability by Payment Initiation API
During the migration, payment types are moved incrementally from the legacy (v8) PSD2 Payment Initiation API to the new Private and Corporate APIs (v1). The table below shows current environment availability per payment type.
For each payment type, availability in production in the new API means that the same payment type in the legacy PSD2 Payment Initiation API enters its deprecation phase.

### Private

| Payment Type                           | Payment Type ID (v8)                            | PSD2 Payment Initiation (v8)       | Payment Type ID (v1)                       | Private PSD2 Payment Initiation (v1) |
|----------------------------------------|-------------------------------------------------|------------------------------------|--------------------------------------------|--------------------------------------|
| Swedish domestic credit transfer       | swedish-domestic-private-credit-transfers       | Production (Deprecated 2026-08-28) | private-se-domestic-credit-transfers       | Production                           |
| Transfers between own Swedish accounts | swedish-domestic-private-own-accounts-transfers | Production (Deprecated 2026-08-28) | private-se-domestic-own-credit-transfers   | Production                           |
| Swedish domestic Bankgiro payment      | swedish-domestic-private-bankgiros              | Production (Deprecated 2026-11-26) | private-se-domestic-alias-credit-transfers | Production                           |
| Swedish domestic PlusGiro payment      | swedish-domestic-private-plusgiros              | Production (Deprecated 2026-11-26) | private-se-domestic-alias-credit-transfers | Production                           |
| SEPA credit transfer                   | sepa-credit-transfers                           | Production (Deprecated 2026-11-26) | private-sepa-credit-transfers              | Production                           |
| Cross-border credit transfer           | cross-border-credit-transfers                   | Production                         | TBA                                        | TBA                                  |


### Corporate

| Payment Type                       | Payment Type ID (v8)           | PSD2 Payment Initiation (v8)       | Payment Type ID (v1)                         | Corporate PSD2 Payment Initiation (v1) |
|------------------------------------|--------------------------------|------------------------------------|----------------------------------------------|----------------------------------------|
| Instant SEPA credit transfer       | —                              | —                                  | corporate-instant-sepa-credit-transfers      | Production                             |
| Swedish domestic credit transfer   | se-domestic-credit-transfers   | Production (Deprecated 2026-08-28) | corporate-se-domestic-credit-transfers       | Production                             |
| Swedish domestic Bankgiro payment  | se-domestic-credit-transfers   | Production (Deprecated 2026-11-26) | corporate-se-domestic-alias-credit-transfers | Production                             |
| Swedish domestic PlusGiro payment  | se-domestic-credit-transfers   | Production (Deprecated 2026-11-26) | corporate-se-domestic-alias-credit-transfers | Production                             |
| SEPA credit transfer               | sepa-credit-transfers          | Production (Deprecated 2026-11-26) | corporate-sepa-credit-transfers              | Production                             |
| Cross-border credit transfer       | cross-border-credit-transfers  | Production                         | TBA                                          | TBA                                    |
| High-value credit transfer         | high-value-credit-transfers    | Production                         | TBA                                          | TBA                                    |
| Danish domestic credit transfer    | dk-domestic-credit-transfers   | Production                         | TBA                                          | TBA                                    |
| Intra-company transfer             | intra-company-credit-transfers | Production                         | TBA                                          | TBA                                    |
| Norwegian domestic credit transfer | no-domestic-credit-transfers   | Production                         | TBA                                          | TBA                                    |
| Polish domestic credit transfer    | pl-domestic-credit-transfers   | Production                         | TBA                                          | TBA                                    |
| UK domestic credit transfer        | uk-domestic-credit-transfers   | Production                         | TBA                                          | TBA                                    |
