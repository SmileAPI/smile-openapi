# API product request and response examples

Examples are grouped as follows:

```text
examples/<product>/<template-id>/request.json
examples/<product>/<template-id>/response.json
```

`verification/default` is used because the Verification request schema has no
`templateId`.

| Product                 | Endpoint                                     | Templates                                                                   |
|-------------------------|----------------------------------------------|-----------------------------------------------------------------------------|
| CreditLifecycle         | `POST /beta/signals` (Signal1)               | `tpl-sgn003001`, deprecated `signalTpl-f250f305c3bf0aa690cca93ef0f0fb03`   |
| BorrowerScreening       | `POST /beta/signals/createSignal2` (Signal2) | `tpl-sgn002001`                                                             |
| Social Security Signals | `POST /beta/signals/createSignal3` (Signal3) | `tpl-sgn003002`, `tpl-social-securities-signal-th`                          |
| Blacklist               | `POST /alpha/blacklists`                     | `tpl-blk002001`, deprecated `blacklistTpl-f29e992a970f4dbbbf9df3cdfec4cd4e` |
| DigitFootprints         | `POST /alpha/footprints`                     | `tpl-email-footprint`, `tpl-mobile-footprint`, `tpl-score-footprint`        |
| Maw                     | `POST /beta/maws/requestMaw2`                | `tpl-maw002001`                                                             |
| BorrowerBehavior        | `POST /beta/maws/requestMaw3`                | `tpl-maw004001`, `tpl-maw004002`, `tpl-maw004003`                           |
| Income Estimator        | `POST /incomes/alpha/incomeestimators`       | `tpl-incomeestimator-001`                                                   |
| Social Security         | `POST /beta/socialSecurities`                | `tpl-sss003002`                                                             |
| Verification            | `POST /alpha/verifications`                  | No template (`default`)                                                     |

The JSON files in this directory are the source for the examples in the English
and Chinese OpenAPI path definitions. Run the sync tool from the repository root
after changing these JSON files:

```shell
ruby tools/sync_api_examples.rb
```

Templates without a directory under `examples/<product>` are not synchronized.
