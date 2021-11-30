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
    implementation 'TODO'
}
```
# Usage

From an Activity/Fragment -
Create a variable

```kotlin
class MainActivity : AppCompatActivity() {

    private val paymentResult = registerForActivityResult(ActivityResultContracts.StartActivityForResult()) {
        when (it.resultCode) {
            RESULT_OK -> {
                //Here the payment is finished successfully.
                Toast.makeText(this, it.data?.getStringExtra(PAYMENT_RESULT) ?: "Payment Successful!", Toast.LENGTH_LONG).show()
            }
            RESULT_CANCELED -> {
                //The user cancels the payment
                Toast.makeText(this, it.data?.getStringExtra(PAYMENT_RESULT) ?: "Payment Failed", Toast.LENGTH_LONG).show()
            }
            else -> {
                //An unknown error has occurred
                Toast.makeText(this, "Unknown Error", Toast.LENGTH_LONG).show()
            }
        }
    }
    //Rest of your code
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

enum class Currency {
    TND,
    EUR,
    USD
}

enum class Language {
    Fr,
    En
}
```

Then in an ```setOnClickListener``` (or anything else you like) pass the class paymentParams:

```kotlin
 val intent = Intent(this, PaymentActivity::class.java)
 intent.putExtra("paymentParams", paymentParams)
 paymentResult.launch(intent)
```
