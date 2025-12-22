| Исходное состояние       | Переходное состояние     | Событие                  | Транзакция                    |
|--------------------------|--------------------------|--------------------------|-------------------------------|
| `CREATED`                | `AWAITING_FRAUD_CHECK`   | `PaymentCreated`         | `CREATE_PAYMENT`              |
| `AWAITING_FRAUD_CHECK`   | `FRAUD_APPROVED`         | `FraudCheckApproved`     | `PERFORM_FRAUD_CHECK`         |
| `AWAITING_FRAUD_CHECK`   | `FRAUD_DENIED`           | `FraudCheckDenied`       | `PERFORM_FRAUD_CHECK`         |
| `AWAITING_FRAUD_CHECK`   | `AWAITING_MANUAL_REVIEW` | `ManualReviewRequired`   | `SUBMIT_MANUAL_REVIEW`        |
| `AWAITING_MANUAL_REVIEW` | `FRAUD_APPROVED`         | `ManualReviewApproved`   | `SUBMIT_MANUAL_REVIEW`        |
| `AWAITING_MANUAL_REVIEW` | `FRAUD_DENIED`           | `ManualReviewDenied`     | `SUBMIT_MANUAL_REVIEW`        |
| `AWAITING_MANUAL_REVIEW` | `FRAUD_APPROVED`         | `ManualReviewTimeout`    | `APPLY_AUTO_APPROVAL_TIMEOUT` |
| `FRAUD_APPROVED`         | `AWAITING_CAPTURE`       | `FundsBlocked`           | `BLOCK_CLIENT_FUNDS`          |
| `AWAITING_CAPTURE`       | `CAPTURED`               | `CaptureSuccessful`      | `CAPTURE_FUNDS`               |
| `AWAITING_CAPTURE`       | `AWAITING_REFUND`        | `CaptureFailed`          | `RELEASE_HOLD`                |
| `CAPTURED`               | `TRANSFERRED`            | `TransferSuccessful`     | `TRANSFER_TO_CONTRAGENT`      |
| `CAPTURED`               | `AWAITING_REFUND`        | `TransferFailed`         | `REFUND_CLIENT_FUNDS`         |
| `TRANSFERRED`            | `COMPLETED`              | `AccountingCompleted`    | `MAKE_ACCOUNTING_ENTRY`       |
| `TRANSFERRED`            | `AWAITING_REFUND`        | `SecurityAlert`          | `REVERSE_CONTRAGENT_TRANSFER` |
| `FRAUD_DENIED`           | `AWAITING_REFUND`        | `RefundInitiated`        | `RELEASE_HOLD`                |
| `AWAITING_REFUND`        | `REFUNDED`               | `RefundCompleted`        | `REFUND_CLIENT_FUNDS`         |
| `COMPLETED`              | `COMPLETED`              | `NotificationSent`       | `NOTIFY_SUCCESS`              |
| `REFUNDED`               | `REFUNDED`               | `RefundNotificationSent` | `NOTIFY_DECLINE`              |
