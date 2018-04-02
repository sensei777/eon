# Slider

## Introduction
Form component that allows to select a value from a range of values by moving the slider thumb of the vc-slider. This can be horizontal or vertical and the value can be visible or not.

To use it import vc-slider in the head of the HTML document:
``` [html]
<head>
  <script>
    vComet.import("/vComet/ui/vc-slider.html");
  </script>
<head>
```

## Declarative usage
To declace a basic vc-slider it is only necessaty to indicate the `name`, because by default the minumum value is 0 and the maximum value is 100. The value in whitch it is located by default is 50.
``` [html]
<vc-slider name="mySlider"></vc-slider>
```

## Programmatic usage
Programmatically, as it happens declaratively, it is only necessary to indicate the `name` and append the vc-slider to the part of the document where it is necessary.
``` [javascript]
vcomet.onReady(function () {
  // Create vc-slider
  var mySlider = document.createElement("vc-slider");

  // Set property and append vc-slider
  slider.name = "mySlider";
  document.querySelector("body").appendChild(mySlider);
});
```

## Examples

### Vertical slider
By default in a vc-slider that has the visible value, it will be placed under the slider.
``` [html]
<vc-slider name="mySlider" min="50" max="200" value="70" orientation="vertical" display-visibility="true"></vc-slider>
```

### Enable dynamically
In this example the vc-slider is contained within a vc-form, and is disabled, and after a second it will be enabled.
``` [html]
<!-- Initially slider disable -->
<vc-slider id="mySlider" name="mySlider" disable="true"></vc-slider>
<vc-button type="submit" value="Submit"></vc-button>

```

``` [javascript]
vcomet.onReady(function () {
  var mySlider = document.querySelector("#mySlider");

  setTimeout(function () {
    // Enables the slider
    mySlider.disable = "false";
  }, 1000);
});
```