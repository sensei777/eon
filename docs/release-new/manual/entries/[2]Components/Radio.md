# Radio

## Introduction
Selectable form component that depends on vc-radiogroup.

If this component was to be used alone it would be needed to import it. But if it would be used among other vc-radio components inside a vc-radiogroup it won't be necessary to import this components as vc-radiogroup will take care of that.
``` [html]
<head>
  <script>
    vComet.import("/vComet/ui/vc-radio.html");
  </script>
<head>
```

## Declarative usage
``` [html]
<vc-radiogroup name="myRadiogroup">
  <vc-radio label="Radio 1" value="myRadio1"></vc-radio>
  <vc-radio label="Radio 2" value="myRadio2"></vc-radio>
</vc-radiogroup>
```

## Programmatic usage
``` [javascript]
vcomet.onReady(function () {
  // Create vc-radiogroup and vc-radio 
  var myRadiogroup = document.createElement("vc-radiogroup");
  var myRadio1 = document.createElement("vc-radio");
  var myRadio2 = document.createElement("vc-radio");

  // Set property and append vc-radiogroup
  myRadiogroup.name = "myRadiogroup";
  document.querySelector(".example").appendChild(myRadiogroup);

  // Set properties of myRadio1
  myRadio1.label = "Radio 1";
  myRadio1.value = "myRadio1";
      
  // Set properties of myRadio2
  myRadio2.label = "Radio 2";
  myRadio2.value = "myRadio2";

  // Append all vc-checkbox
  myRadiogroup.appendChild(myRadio1);
  myRadiogroup.appendChild(myRadio2);
});
```

## Examples

### Enable and check dynamically
In this example one of the vc-radio is disable and other is checked, but after a second the disable and unchecked radio will be enable and checked.
``` [html]
<vc-radiogroup name="myRadiogroup">
  <!-- Initially radio checked -->
  <vc-radio label="Radio 1" value="myRadio1" check="true"></vc-radio>
  <!-- Initially radio disable -->
  <vc-radio id="myRadio2" label="Radio 2" value="myRadio2" disable="true"></vc-radio>
</vc-radiogroup>
```

``` [javascript]
vcomet.onReady(function () {
  var myRadio2 = document.querySelector("#myRadio2");

  setTimeout(function () {
    // Set new values of properties
    myRadio2.check = true;
    myRadio2.disable = false;
  }, 1000);
});
```