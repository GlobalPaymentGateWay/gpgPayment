# GpgPayment
This library makes it easy to integrate payment in mobile apps.

## Install

Include the JitPack.io Maven repo in your project's build.gradle file

```groovy
allprojects {
 repositories {
    maven { url "https://jitpack.io" }
 }
}
```

Then add this dependency to your app's build.gradle file

```groovy
dependencies {
    implementation 'com.github.tapadoo:alerter:$current-version'
}
```
# Usage

From an Activity -
Create a variable

```kotlin
    private val paymentResult = registerForActivityResult(ActivityResultContracts.StartActivityForResult()) {
        when (it.resultCode) {
            RESULT_OK -> {
                Toast.makeText(this, it.data?.getStringExtra(PAYMENT_RESULT) ?: "Payment Successful!", Toast.LENGTH_LONG).show()
            }
            RESULT_CANCELED -> {
                Toast.makeText(this, it.data?.getStringExtra(PAYMENT_RESULT) ?: "Payment Failed", Toast.LENGTH_LONG).show()
            }
            else -> {
                Toast.makeText(this, "Unknown Error", Toast.LENGTH_LONG).show()
            }
        }
    }
```

Create an instance of the class PaymentParams and fill it with your data
```kotlin
data class PaymentParams(
    val numSite: String,
    val password: String,
    val orderId: String,
    val customerEmail: String,
    val customerLastName: String,
    val customerFirstName: String,
    val customerAddress: String,
    val customerZip: String? = null,
    val customerCity: String? = null,
    val customerCountry: String? = null,
    val customerTel: String,
    val language: Language,
    val amount: Long,
    val amountSecond: Long? = null,
    val currency: Currency,
    val paymentType: Boolean,
    val orderProducts: String,
    val signature: String,
    val vad: String,
    val terminal: String,
    val tauxConversion: Float?,
    val batchNumber: String? = null,
    val merchantReference: String? = null,
    val merchantUserName: String,
    val merchantPassword: String
)
```

then in an on click listener(or anything else you like) pass the class paymentParams

```kotlin
            val intent = Intent(this, PaymentActivity::class.java)
            intent.putExtra("paymentParams", paymentParams)
            paymentResult.launch(intent)
```
