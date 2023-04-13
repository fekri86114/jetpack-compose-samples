# jetpack-compose-samples
*Use these code-samples to practice the Jetpack Compose!*

### ___

    @SuppressLint("UnusedMaterialScaffoldPaddingParameter")
    @Composable
    fun ScaffoldDemo() {
        val materialBlue700 = Color(0xFF1976D2)
        val scaffoldState = rememberScaffoldState(rememberDrawerState(DrawerValue.Closed))
        Scaffold(
            scaffoldState = scaffoldState,
            topBar = {
                TopAppBar(title = {
                    Text(
                        "TopAppBar",
                        fontSize = 30.sp,
                        style = TextStyle(color = Color.White)
                    )
                }, backgroundColor = materialBlue700)
            },
            floatingActionButtonPosition = FabPosition.End,
            floatingActionButton = {
                FloatingActionButton(onClick = {}) {
                    Text("X")
                }
            },
            drawerContent = { Text(text = "drawerContent") },
            content = { Text("BodyContent") },
            bottomBar = { BottomAppBar(backgroundColor = materialBlue700) { Text("BottomAppBar") } }
        )
    }

---

    @Composable
    fun ColumnExample() {
        Column(
            modifier = Modifier
                .width(100.dp)
                .padding(4.dp)
                .background(Color.LightGray),
            verticalArrangement = Arrangement.Center,
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
            Text(text = "Hello, World!")
            Text(text = "Hello, World!2")
        }
    }

---

    @Composable
    fun RowExample() {
        Row(
            horizontalArrangement = Arrangement.SpaceEvenly,
            modifier = Modifier.fillMaxWidth()
        ) {
            Text(text = "Hello, world!")
            Text(text = "Hello, world!2")
        }
    }

---

    @Composable
    fun BoxExample() {
        Box(modifier = Modifier.fillMaxSize()) {
            Text(
                text = "This text is write first",
                modifier = Modifier
                    .align(Alignment.TopCenter)
                    .padding(top = 8.dp)
            )
            Box(
                modifier = Modifier
                    .align(Alignment.TopCenter)
                    .background(Color.Green)
                    .fillMaxHeight()
                    .width(50.dp)
            )
            Text(text = "This text is write last", modifier = Modifier.align(Alignment.Center))
            FloatingActionButton(
                modifier = Modifier
                    .align(Alignment.BottomEnd)
                    .padding(12.dp),
                onClick = {}
            ) {
                Text("+")
            }
        }
    }

---

    @Composable
    fun CanvasDrawExample() {
        Canvas(modifier = Modifier.fillMaxSize()) {
            drawRect(Color.Blue, topLeft = Offset(0f, 0f), size = Size(this.size.width, 55f))
            drawCircle(Color.Red, center = Offset(100f, 200f), radius = 80f)
            drawLine(
                Color.Green, Offset(20f, 0f),
                Offset(200f, 200f), strokeWidth = 5f
            )
            drawArc(
                Color.Black,
                0f,
                60f,
                useCenter = true,
                size = Size(300f, 300f),
                topLeft = Offset(60f, 60f)
            )
        }
    }

---

    @Composable
    fun ImageResourceDemo() {
        val image: Painter = painterResource(id = R.drawable.composelogo)
        Image(painter = image, contentDescription = "Compose logo")
    }

---

    @Composable
    fun LazyColumnDemo() {
        val list = listOf<String>("A", "B", "C", "D") + ((0..100).map { it.toString() })

        LazyColumn(modifier = Modifier.fillMaxHeight()) {
            items(items = list, itemContent = { item ->
                Log.d("COMPOSE", "This get rendered $item")
                when (item) {
                    "A" -> {
                        Text(text = item, style = TextStyle(fontSize = 80.sp))
                    }
                    "B" -> {
                        Button(onClick = {}) {
                            Text(text = item, style = TextStyle(fontSize = 80.sp))
                        }
                    }
                    "C" -> {
                        // do nothing
                    }
                    "D" -> {
                        Text(text = item)
                    }
                    else -> {
                        Text(text = item, style = TextStyle(fontSize = 80.sp))
                    }
                }
            })
        }
    }

---

    @Composable
    fun LazyRowDemo() {
        val list = listOf<String>("A", "B", "C", "D") + ((0..100).map { it.toString() })

        LazyRow(modifier = Modifier.fillMaxHeight()) {
            items(items = list, itemContent = { item ->
                Log.d("ComposeLog", "This get rendered $item")
                when (item) {
                    "A" -> {

                    }
                    "B" -> {
                        Button(onClick = {}) {
                            Text(text = item, style = TextStyle(fontSize = 80.sp))
                        }
                    }
                    "C" -> {
                        //Do Nothing
                    }
                    "D" -> {
                        Text(text = item)
                    }
                    else -> {
                        Text(text = item, style = TextStyle(fontSize = 80.sp))
                    }
                }
            })
        }
    }

---

    @Composable
    fun LazyVerticalGridDemo() {
        val list = (1..10).map { it.toString() }

        LazyVerticalGrid(
            columns = GridCells.Fixed(2),
            contentPadding = PaddingValues(
                start = 12.dp,
                top = 16.dp,
                end = 12.dp,
                bottom = 16.dp
            ),
            content = {
                items(list.size) { index ->
                    Card(
                        backgroundColor = Color.Red,
                        modifier = Modifier
                            .padding(4.dp)
                            .fillMaxWidth(),
                        elevation = 8.dp
                    ) {
                        Text(
                            text = list[index],
                            fontWeight = FontWeight.Bold,
                            fontSize = 30.sp,
                            color = Color(0xFFFFFFFF),
                            textAlign = TextAlign.Center,
                            modifier = Modifier.padding(16.dp)
                        )
                    }
                }
            }
        )
    }

---

    @Composable
    fun RectangleShapeDemo() {
        ExampleBox(shape = CutCornerShape(8.dp))
    }

    @Composable
    fun ExampleBox(shape: Shape) {
        Column(
            modifier = Modifier
                .fillMaxWidth()
                .wrapContentSize(Alignment.Center)
                .padding(8.dp)
        ) {
            Box(
                modifier = Modifier
                    .size(100.dp)
                    .clip(shape)
                    .background(Color.Red)
            )
        }
    }

---

    @Composable
    fun TextExample() {
        Column {
            Text(text = "Just a Text")
            Text(text = "Text with Cursive font", style = TextStyle(fontFamily = FontFamily.Cursive))
            Text(
                text = "Text with LineThrough",
                style = TextStyle(textDecoration = TextDecoration.LineThrough)
            )
            Text(
                text = "Text with Underline",
                style = TextStyle(textDecoration = TextDecoration.Underline)
            )
            Text(
                text = "Text with Underline, LineThrough and bold",
                style = TextStyle(
                    textDecoration = TextDecoration.combine(
                        listOf(
                            TextDecoration.LineThrough,
                            TextDecoration.Underline
                        )
                    ),
                    fontWeight = FontWeight.Bold
                )
            )
        }
    }

---

    @Composable
    fun AlertDialogSample() {
        MaterialTheme {
            Column {
                val openDialog = remember { mutableStateOf(false) }

                Button(onClick = { openDialog.value = true }) {
                    Text(text = "Click me!")
                }

                if (openDialog.value) {

                    AlertDialog(
                        onDismissRequest = { openDialog.value = false },
                        title = { Text(text = "Dialog Title") },
                        text = { Text(text = "Here's a Text!") },
                        confirmButton = {
                            Button(
                                onClick = { openDialog.value = false }
                            ) {
                                Text(text = "Confirm")
                            }
                        },
                        dismissButton = {
                            Button(
                                onClick = { openDialog.value = false }
                            ) {
                                Text(text = "Dismiss")
                            }
                        }
                    )

                }
            }
        }
    }

 ---

    @Composable
    fun ButtonExample() {
        Button(
            onClick = { /*Do something!*/ },
            colors = ButtonDefaults.buttonColors(backgroundColor = Color.Yellow)
        ) {
            Text(text = "Button")
        }
    }

---

    @Composable
    fun OutlinedButtonExample() {
        OutlinedButton(onClick = { /*Do something!*/ }) {
            Text(text = "Outlined button!")
        }
    }

---

    @Composable
    fun TextButtonExample() {
        TextButton(onClick = { /*Do something*/ }) {
            Text(text = "TextButton!")
        }
    }

---

    @Composable
    fun CheckBoxDemo() {
        val checkedState = remember { mutableStateOf(true) }

        Checkbox(
            checked = checkedState.value,
            onCheckedChange = {
                checkedState.value = it
            }
        )
    }

---

    @Composable
    fun CircularProgressIndicatorSample() {
        var progress by remember { mutableStateOf(0.1f) }
        val animatedProgress = animateFloatAsState(
            targetValue = progress,
            animationSpec = ProgressIndicatorDefaults.ProgressAnimationSpec
        ).value

        Column(horizontalAlignment = Alignment.CenterHorizontally) {
            Spacer(modifier = Modifier.height(30.dp))
            Text("CircularProgressIndicator with undefined progress")
            CircularProgressIndicator()

            Spacer(modifier = Modifier.height(30.dp))
            Text("CircularProgressIndicator with progress set by buttons")
            CircularProgressIndicator(progress = animatedProgress)

            Spacer(modifier = Modifier.height(30.dp))
            OutlinedButton(
                onClick = {
                    if (progress < 1f) progress += 0.1f
                }
            ) {
                Text(text = "Increase")
            }
            OutlinedButton(
                onClick = {
                    if (progress > 0f) progress -= 0.1f
                }
            ) {
                Text(text = "Decrease")
            }
        }
    }

---

    @Composable
    fun DropdownDemo() {
        var expanded by remember { mutableStateOf(false) }
        val items = listOf<String>("A", "B", "C", "D", "E")
        val disabledValue = "B"
        var selectedIndex by remember { mutableStateOf(0) }

        Box(
            modifier = Modifier
                .fillMaxSize()
                .wrapContentSize(Alignment.TopStart)
        ) {
            Text(
                text = items[selectedIndex],
                modifier = Modifier
                    .fillMaxWidth()
                    .clickable { expanded = true }
                    .background(Color.Gray)
            )
            DropdownMenu(
                expanded = expanded,
                onDismissRequest = { expanded = false },
                modifier = Modifier
                    .fillMaxWidth()
                    .background(Color.Red)
            ) {
                items.forEachIndexed { index, s ->
                    DropdownMenuItem(
                        onClick = {
                            selectedIndex = index
                            expanded = false
                        }
                    ) {
                        val disabledText = if (s == disabledValue) " (Disabled)" else ""
                        Text(text = s + disabledText)
                    }
                }
            }
        }
    }

---

    @Composable
    fun FloatingActionButtonDemo() {
        FloatingActionButton(onClick = { /*do something*/ }) {
            Text(text = "FloatingActionButton", modifier = Modifier.padding(8.dp))
        }
    }

---

    @Composable
    fun ExtendedFloatingActionButtonDemo() {
        ExtendedFloatingActionButton(
            text = { Text(text = "ExtendedFloatingActionButton") },
            icon = { Icon(Icons.Filled.Favorite, "") },
            onClick = { /*do something*/ },
            elevation = FloatingActionButtonDefaults.elevation(8.dp)
        )
    }

---

    @Composable
    fun ModalDrawerSample() {
        val drawerState = rememberDrawerState(initialValue = DrawerValue.Closed)
        val scope = rememberCoroutineScope()

        ModalDrawer(
            drawerState = drawerState,
            drawerContent = {
                Column {
                    Text(text = "Text in drawer")
                    Button(
                        onClick = {
                            scope.launch { drawerState.close() }
                        }
                    ) {
                        Text(text = "Close!")
                    }
                }
            },
            content = {
                Column {
                    Text(text = "Text in BodyContext")
                    Button(
                        onClick = {
                            scope.launch { drawerState.open() }
                        }
                    ) {
                        Text(text = "Open!")
                    }
                }
            }
        )
    }

---

    @Composable
    fun RadioButtonSample() {
        val radioOptions = listOf<String>("A", "B", "C")
        val (selectedOption, onOptionSelected) = remember { mutableStateOf(radioOptions[1]) }

        Column {
            radioOptions.forEach { text ->
                Row(
                    Modifier
                        .fillMaxWidth()
                        .selectable(
                            selected = (text == selectedOption),
                            onClick = {
                                onOptionSelected(text)
                            }
                        )
                        .padding(horizontal = 16.dp)
                ) {
                    RadioButton(
                        selected = (text == selectedOption),
                        onClick = { onOptionSelected(text) }
                    )
                    Text(
                        text = text,
                        style = MaterialTheme.typography.body1.merge(),
                        modifier = Modifier.padding(start = 16.dp)
                    )
                }
            }
        }
    }

---

    @Composable
    fun MySliderDemo() {
        var sliderPosition by remember { mutableStateOf(0f) }
        Text(text = sliderPosition.toString())
        Slider(value = sliderPosition, onValueChange = { sliderPosition = it })
    }

---

    @Composable
    fun SnackbarDemo() {
        Column {
            val (snackBarVisibleState, setSnackBarState) = remember { mutableStateOf(false) }

            Button(
                onClick = {
                    setSnackBarState(!snackBarVisibleState)
                }
            ) {
                if (snackBarVisibleState) {
                    Text(text = "Hide!")
                } else {
                    Text(text = "Show!")
                }
            }
            if (snackBarVisibleState) {
                Snackbar(
                    action = {
                        Button(onClick = { }) {
                            Text(text = "My Action")
                        }
                    },
                    modifier = Modifier.padding(8.dp)
                ) {
                    Text(text = "This is a Snackbar!")
                }
            }
        }
    }

---

    @Composable
    fun SwitchDemo() {
        val checkedState = remember { mutableStateOf(true) }

        Switch(
            checked = checkedState.value,
            onCheckedChange = { checkedState.value = it }
        )
    }

---

    @Composable
    fun TextFieldDemo() {
        Column(modifier = Modifier.padding(16.dp)) {
            val textState = remember { mutableStateOf(TextFieldValue()) }

            TextField(value = textState.value, onValueChange = { textState.value = it })
            Text(text = "The textfield has this text: ${textState.value.text}")
        }
    }
    
### ___

***I hope you enjoy!!✌😋😍😍***

