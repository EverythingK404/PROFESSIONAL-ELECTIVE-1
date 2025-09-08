package com.exercise.assignment1_activitylifecycle

import android.os.Bundle
import android.util.Log
import android.widget.Toast
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.enableEdgeToEdge
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.padding
import androidx.compose.material3.Scaffold
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.tooling.preview.Preview
import com.exercise.assignment1_activitylifecycle.ui.theme.Assignment1ActivityLifecycleTheme

class MainActivity : ComponentActivity() {

    companion object {
        private const val TAG = "MainActivityLifecycle"
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        Log.d(TAG, "onCreate")
        Toast.makeText(this, "onCreate", Toast.LENGTH_SHORT).show()

        enableEdgeToEdge()
        setContent {
            Assignment1ActivityLifecycleTheme {
                Scaffold(modifier = Modifier.fillMaxSize()) { innerPadding ->
                    Greeting(
                        name = "ALDUB NATION",
                        modifier = Modifier.padding(innerPadding)
                    )
                }
            }
        }
    }

    override fun onStart() {
        super.onStart()
        Log.d(TAG, "onStart")
        Toast.makeText(this, "oStart", Toast.LENGTH_SHORT).show()
    }

    override fun onResume() {
        super.onResume()
        Log.d(TAG, "onResume")
        Toast.makeText(this, "onResume", Toast.LENGTH_SHORT).show()
    }

    override fun onPause() {
        super.onPause()
        Log.d(TAG, "onPause")
        Toast.makeText(this, "onPause", Toast.LENGTH_SHORT).show()
    }

    override fun onStop() {
        super.onStop()
        Log.d(TAG, "onStop")
        Toast.makeText(this, "onStop", Toast.LENGTH_SHORT).show()
    }

    override fun onDestroy() {
        super.onDestroy()
        Log.d(TAG, "onDestroy")
        Toast.makeText(this, "onDestroy", Toast.LENGTH_SHORT).show()
    }

    override fun onRestart() {
        super.onRestart()
        Log.d(TAG, "onRestart")
        Toast.makeText(this, "onRestart", Toast.LENGTH_SHORT).show()
    }
}

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello $name!",
        modifier = modifier
    )
}

@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    Assignment1ActivityLifecycleTheme {
        Greeting("ALDUB NATION")
    }
}
