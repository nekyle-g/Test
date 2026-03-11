<LinearLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp"
    android:gravity="center">

    <EditText
        android:id="@+id/scoreInput"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Score (0-100)"
        android:inputType="number" />

    <Button
        android:id="@+id/rankButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Check Rank"
        android:layout_marginTop="10dp"/>

    <TextView
        android:id="@+id/resultText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="20sp"
        android:layout_marginTop="20dp"
        android:textStyle="bold"/>
</LinearLayout>




import android.os.Bundle
import android.widget.Button
import android.widget.EditText
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val scoreInput = findViewById<EditText>(R.id.scoreInput)
        val rankButton = findViewById<Button>(R.id.rankButton)
        val resultText = findViewById<TextView>(R.id.resultText)

        rankButton.setOnClickListener {
            val inputText = scoreInput.text.toString()
            
            // 1. Check if input is empty or not a number
            val score = inputText.toIntOrNull()

            // 2. Error handling for null or scores > 100
            if (score == null || score > 100 || score < 0) {
                resultText.text = "❌ Error: Please enter a valid number between 0 and 100."
                return@setOnClickListener
            }

            // 3. Logic for low scores (If Statement)
            if (score < 10) {
                resultText.text = "Score: $score \nWas the controller even plugged in? Try again! 🎮"
            } 
            // 4. Logic for ranks (When Statement)
            else {
                val rank = when (score) {
                    in 10..19 -> "Noob"
                    in 20..49 -> "Casual"
                    in 50..79 -> "Pro"
                    else -> "Legendary" // Covers 80-100
                }
                resultText.text = "Rank: $rank"
            }
        }
    }
}
