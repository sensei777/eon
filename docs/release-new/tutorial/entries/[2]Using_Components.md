# Using Components
In this tutorial we are going to make a simple To Do List to teach you about the most basic components vComet offers, and to show you how easy it is getting used to them.

## Import components
To create the To Do List we are going to use 4 components only:  `vc-text`, `vc-button`, `vc-checkbox` and `vc-scroll`. The first thing do is import them into the html file:

```[html]
<script>
    vcomet.import([
        "vcomet/ui/vc-text.html",
        "vcomet/ui/vc-button.html",
        "vcomet/ui/vc-checkbox.html",
        "vcomet/ui/vc-scroll.html"
    ]);
</script>
```

 ## Declare components
 We are going to declare components that will be loaded with the document, that is, those that are not created by the user interaction. In order to do this, we are going to use HTML tags, but with vComet nomenclature.

```[html]
<div class="main">
    <div class="absoluteContainer">
        <vc-scroll arrowScrolls="true">
            <div class="todoContainer">
                <span class="title">To Do list</span>

                <!-- It will contain the elements to the list that are added. -->
                <div class="listContainer"></div>

                <!-- Sending data section container-->
                <div class="setNewContainer">
                    <!-- Component to input the text we want to add into the list -->
                    <vc-text class="addItem" name="addItem" type="text" placeholder="New Item"></vc-text>
                    
                    <!-- Button to add the text to the list. In the onclick we name the function to add the text. -->
                    <vc-button class="addButton" value="Add" expand="inline" onclick="addItem();"></vc-button>
                </div>
            </div>
        </vc-scroll>
    </div>
</div>
```

 ## Dynamic components
 Once the static components are declared, we establish dynamic functionality in order to add the list items.

 The button for adding the new item will call the `addItem()` function, which will store the vc-text input value and send it to the `setValue()` function.
``` [javascript]
function addItem() {
    var textbox = document.querySelector("vc-text");
    var textboxValue = textbox.value;

    if (textboxValue != "") {
        // Call function to set the new list item
        setItem(textboxValue);

        // Reestablishes the vc-text value
        textbox.setValue("");
        textbox.value = "";
    }

}
```

With this function we dinamically create the required components that will be into the list item. 
To use vComet programmatically we will do it inside the 'onReady' event, to be sure that all 
the functionalities are loaded in the document.
``` [javascript]
function setItem(newItem) {
    vcomet.onReady(function () {
        // We create a checkbox that will be the item in the list 
        var newCheckbox = document.createElement("vc-checkbox");
        // We add a button to edit the item
        var newEdit = document.createElement("vc-button");
        // We add a button to delete the item from the list
        var newDelete = document.createElement("vc-button");
        // newItemContainer is the node that will be contain the item
        var newItemContainer = document.createElement("div");
        var listContainer = document.querySelector(".listContainer");
        // This node will contain the default view of the item 
        var defaultContainer = document.createElement("div");

        // Set properties of checkbox item
        newCheckbox.classList.add("checkboxItem");
        newCheckbox.label = newItem;
        newCheckbox.value = newItem;

        // Edit item button
        newEdit.classList.add("editButton");
        newEdit.icon = '<i class="material-icons">mode_edit</i>';
        // Set the call to function to edit the value of the checkbox item
        newEdit.setOnClick("editItem(this.parentNode.parentNode);");

        // Delete item button properties
        newDelete.classList.add("deleteButton");
        newDelete.icon = '<i class="material-icons">close</i>';
        // Set the call to function to delete the node that contains the item
        newDelete.setOnClick("deleteItem(this.parentNode.parentNode);");

        // Append newItemContainer to listContainer
        listContainer.appendChild(newItemContainer);

        newItemContainer.classList.add("newItemContainer");
        // Append newCheckbox, newEdit and newDelete to newItemContainer 
        defaultContainer.appendChild(newCheckbox);
        defaultContainer.appendChild(newEdit);
        defaultContainer.appendChild(newDelete);

        newItemContainer.appendChild(defaultContainer);

        // Register newItemContainer node to be aware if it is on the click path by giving `isOnPath` property
        vcomet.registerPathListener(newItemContainer);
    });
}
```

This function adds dinamically the necessary components for edit the list item.
```[javascript]
function editItem(item) {
    // Stores the item current value
    var itemValue = item.querySelector(".checkboxItem").value;

    item.classList.add("visibleEditor");

    // Editing node does not exist yet
    if (!item.querySelector(".editContainer")) {
        vcomet.onReady(function () {
            // We create a new input text to sent the new item value
            var newItemEdit = document.createElement("vc-text");
            var newSave = document.createElement("vc-button");
            // This node will contain the edit view of the item 
            var editContainer = document.createElement("div");

            editContainer.classList.add("editContainer");

            // Set input text properties
            newItemEdit.classList.add("editText");
            newItemEdit.placeholder = itemValue;

            // Save item button properties
            newSave.classList.add("saveButton");
            newSave.value = 'Save';
            // Call the function for establish the new item valie
            newSave.setOnClick("setEditItem(this.parentNode.parentNode);");

            //  Append newItemEdit and newSave to editContainer
            editContainer.appendChild(newItemEdit);
            editContainer.appendChild(newSave);

            // Append editContainer to the item wrapper
            item.appendChild(editContainer);

            // When you click outside the item, it loses focus and leaves the edit view 
            document.body.addEventListener("click", function (event) {
                // If the click event does not goes through this item the isOnPath property returns false
                if (item.isOnPath != true) {
                    item.classList.remove("visibleEditor");
                }
            }, false);
        });
    }
}
```