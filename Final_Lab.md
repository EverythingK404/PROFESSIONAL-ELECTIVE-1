package com.exercise.mainactivity

import android.os.Bundle
import android.widget.Toast
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.enableEdgeToEdge
import androidx.compose.foundation.Image
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.layout.size
import androidx.compose.foundation.layout.wrapContentSize
import androidx.compose.material3.Button
import androidx.compose.material3.Icon
import androidx.compose.material3.IconButton
import androidx.compose.material3.OutlinedTextField
import androidx.compose.material3.Scaffold
import androidx.compose.material3.Switch
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import com.exercise.mainactivity.ui.theme.MainActivityTheme

import androidx.compose.material3.DropdownMenuItem
import androidx.compose.material3.ExperimentalMaterial3Api
import androidx.compose.material3.ExposedDropdownMenuBox
import androidx.compose.material3.ExposedDropdownMenuDefaults
import androidx.compose.material3.TextField

import androidx.compose.ui.graphics.Color
import androidx.compose.material3.Surface
import androidx.compose.material3.OutlinedTextFieldDefaults
import androidx.compose.material3.ButtonDefaults
import androidx.compose.ui.unit.sp
import androidx.compose.ui.text.font.FontWeight

val Green = Color(0xFF689F38)
val Background = Color(0xFFF0FFF0)
val TextColor = Color(0xFF212121)

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            MainActivityTheme {
                Scaffold(modifier = Modifier.fillMaxSize()) { innerPadding ->
                    Screen(modifier = Modifier.padding(innerPadding))
                }
            }
        }
    }
}

@Composable
fun Screen(modifier: Modifier = Modifier) {

    Surface(
        color = Background,
        modifier = modifier.fillMaxSize()
    ) {
        Column(
            modifier = Modifier.fillMaxSize()
        ) {
            WelcomeLabExercise(
                name = "Welcome to Android UI",
                modifier = Modifier.fillMaxWidth()
            )

            Spacer(modifier = Modifier.height(24.dp))

            TextControlsExercise()

            Spacer(modifier = Modifier.height(32.dp))

            ButtonControlsExercise()

            Spacer(modifier = Modifier.height(32.dp))
            
            ImageControlsExercise() 

        }
    }
}



// Exercise 1: Welcome Lab Exercise

@Composable
fun WelcomeLabExercise(name: String, modifier: Modifier = Modifier) {
    Text(
        text = name,
        color = Green,
        fontSize = 20.sp,
        fontWeight = FontWeight.Bold,
        modifier = modifier
            .fillMaxWidth()
            .padding(top = 24.dp, bottom = 8.dp)
            .wrapContentSize(Alignment.TopCenter)
    )
}


//Exercise 3: Implementing Text Controls

@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun TextControlsExercise(modifier: Modifier = Modifier) {


    var userInput by remember { mutableStateOf("") }
    var isDropdownOpen by remember { mutableStateOf(false) }


    val options = listOf("1st", "2nd", "3rd", "4th", "5th")
    var selectedOption by remember { mutableStateOf(options[0]) }
    var isOptionDropdownOpen by remember { mutableStateOf(false) }



    val countries = listOf("Philippines", "USA", "Mexico")


    val filteredCountries = countries.filter {
        it.startsWith(userInput, ignoreCase = true)
    }


    Column(modifier = modifier.fillMaxWidth().padding(horizontal = 32.dp)) {

        Text(
            text = "Exercise 3: Implementing Text Controls",
            color = TextColor,
            fontWeight = FontWeight.Medium,
            modifier = Modifier.padding(bottom = 8.dp)
        )
        Spacer(modifier = Modifier.height(8.dp))


        Column(modifier = Modifier.fillMaxWidth().padding(horizontal = 16.dp)) {

            Text(
                text = "Type (Philippines, USA, Mexico) for  AutoCompleteTextView:",
                color = TextColor,
                modifier = Modifier.padding(bottom = 8.dp)
            )
            Spacer(modifier = Modifier.height(8.dp))


            ExposedDropdownMenuBox(
                expanded = isDropdownOpen,
                onExpandedChange = {

                    if (filteredCountries.isNotEmpty()) {
                        isDropdownOpen = !isDropdownOpen
                    }
                },
                modifier = Modifier.fillMaxWidth()
            ) {


                OutlinedTextField(
                    modifier = Modifier.menuAnchor().fillMaxWidth(),
                    value = userInput,
                    onValueChange = {
                        userInput = it
                        isDropdownOpen = it.isNotEmpty() && filteredCountries.isNotEmpty()
                    },
                    label = { Text("Search Country", color = TextColor) },
                    colors = OutlinedTextFieldDefaults.colors(
                        unfocusedBorderColor = Green,
                    )
                )

                ExposedDropdownMenu(
                    expanded = isDropdownOpen && filteredCountries.isNotEmpty(),
                    onDismissRequest = { isDropdownOpen = false }
                ) {
                    filteredCountries.forEach { country ->
                        DropdownMenuItem(
                            text = { Text(country) },
                            onClick = {
                                userInput = country
                                isDropdownOpen = false
                            },
                            contentPadding = ExposedDropdownMenuDefaults.ItemContentPadding,
                        )
                    }
                }
            }

            Spacer(modifier = Modifier.height(16.dp))

            Text(
                text = "Spinner with 5 sample options:",
                color = TextColor,
                modifier = Modifier.padding(bottom = 8.dp)
            )


            ExposedDropdownMenuBox(
                expanded = isOptionDropdownOpen,
                onExpandedChange = { isOptionDropdownOpen = !isOptionDropdownOpen },
                modifier = Modifier.fillMaxWidth()
            ) {

                TextField(
                    modifier = Modifier.menuAnchor().fillMaxWidth(),
                    value = selectedOption,
                    onValueChange = { },
                    readOnly = true,
                    trailingIcon = {
                        ExposedDropdownMenuDefaults.TrailingIcon(expanded = isOptionDropdownOpen)
                    },
                    label = { Text("Select Option", color = TextColor) },
                    colors = ExposedDropdownMenuDefaults.textFieldColors(
                        unfocusedIndicatorColor = Green,
                        unfocusedTrailingIconColor = Green,
                    ),
                )


                ExposedDropdownMenu(
                    expanded = isOptionDropdownOpen,
                    onDismissRequest = { isOptionDropdownOpen = false }
                ) {
                    options.forEach { option ->
                        DropdownMenuItem(
                            text = { Text(option) },
                            onClick = {
                                selectedOption = option
                                isOptionDropdownOpen = false
                            },
                            contentPadding = ExposedDropdownMenuDefaults.ItemContentPadding,
                        )
                    }
                }
            }
        }
    }
}


// Exercise 4: Working with Button Controls
@Composable
fun ButtonControlsExercise(modifier: Modifier = Modifier) {

    val context = LocalContext.current

    var isToggled by remember { mutableStateOf(false) }

    Column(modifier = modifier.fillMaxWidth().padding(horizontal = 32.dp)) {

        Text(
            text = "Exercise 4: Working with Button Controls",
            color = TextColor,
            fontWeight = FontWeight.Medium,
            modifier = Modifier.padding(bottom = 8.dp)
        )


        Button(
            onClick = {
                Toast.makeText(context, "Standard Button Clicked!", Toast.LENGTH_SHORT).show()
            },
            colors = ButtonDefaults.buttonColors(containerColor = Green),

            elevation = ButtonDefaults.buttonElevation(defaultElevation = 4.dp),
            modifier = Modifier.fillMaxWidth()
        ) {
            Text("Standard Button", color = Background)
        }

        Spacer(modifier = Modifier.height(16.dp))

        IconButton(
            onClick = {
                Toast.makeText(context, "Image Clicked!", Toast.LENGTH_SHORT).show()
            },
            modifier = Modifier.align(Alignment.CenterHorizontally)
        ) {
            Icon(

                painter = painterResource(id = R.drawable.androidpic),
                contentDescription = "Image button",
                tint = Green,
                modifier = Modifier.height(48.dp)
            )
        }

        Spacer(modifier = Modifier.height(16.dp))


        Row(
            modifier = Modifier.fillMaxWidth().padding(horizontal = 8.dp),
            verticalAlignment = Alignment.CenterVertically,
            horizontalArrangement = Arrangement.SpaceBetween
        ) {
            Text("ToggleButton Status: ${if (isToggled) "ON" else "OFF"}", color = TextColor)
            Switch(
                checked = isToggled,
                onCheckedChange = {
                    isToggled = it
                    Toast.makeText(context, if (it) "ON" else "OFF", Toast.LENGTH_SHORT).show()
                }
                )

        }
    }
}

// Exercise 5: Using Image Controls

@Composable
fun ImageControlsExercise(modifier: Modifier = Modifier) {

    var isFirstImageActive by remember { mutableStateOf(true) }

    val currentImageId = if (isFirstImageActive) {
        R.drawable.androidpic
    } else {
        R.drawable.androidpic2
    }

    Column(
        modifier = modifier.fillMaxWidth().padding(horizontal = 32.dp),
        horizontalAlignment = Alignment.CenterHorizontally
    ) {

        Text(
            text = "Exercise 5: Using Image Controls",
            color = TextColor,
            fontWeight = FontWeight.Medium,
            modifier = Modifier.padding(bottom = 8.dp)
        )

        Image(
            painter = painterResource(id = currentImageId),
            contentDescription = "Dynamically switching Android image",
            modifier = Modifier.size(100.dp)
        )

        Spacer(modifier = Modifier.height(16.dp))


        Button(
            onClick = {
                isFirstImageActive = !isFirstImageActive
            },
            colors = ButtonDefaults.buttonColors(containerColor = Green),

            elevation = ButtonDefaults.buttonElevation(defaultElevation = 4.dp),
            modifier = Modifier.fillMaxWidth()
        )

        {
            Text("Click to Switch Image", color = Background)
        }
    }
}


@Preview(showBackground = true)
@Composable
fun CombinedExercisePreview() {
    MainActivityTheme {
        Screen()
    }
}
