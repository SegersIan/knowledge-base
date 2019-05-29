# OpenUI5

The documentation can be found on [this link](https://openui5.hana.ondemand.com).

OpenUI5 is a javascript client side framework created by the people at SAP with existing components
that come out of the books with different themes. It uses jQuery under the hood and has an
MVC architecture. So think of MVC framework with default themes and designs like bootstrap.

## To remember

### Inheritance

When inheriting an OpenUI5 object to add custom logic, make sure to call also the function on the
prototype chain that you are overriding.

```js
MyClass.prototype.onAfterRendering = function() {
  SuperClass.prototype.onAfterRendering.apply(this);
}
```

### Platform & Browser support

Can be found [here](https://openui5.hana.ondemand.com/#/topic/74b59efa0eef48988d3b716bd0ecc933);

### Cross library usage

![Image](assets/openuilibs.png)

[source](https://openui5.hana.ondemand.com/#/topic/363cd16eba1f45babe3f661f321a7820)

### Releases

Every month, OpenUI5 releases a new version for productive usage. And once per year a new LTS.

### OpenUI5 vs. SAPUI5

OpenUI5 is an OSS licence, SAPUI5 requires a license

### Named Models

Set a model with a key when you have multiple models living in parallel with each other.

```js
 var oBundle = this.getView().getModel("i18n").getResourceBundle();
 var sRecipient = this.getView().getModel().getProperty("/recipient/name");
```

### Data binding

In the XML view, we use data binding to connect the button text to the showHelloButtonText property in the i18n model. 
A resource bundle is a flat structure, therefore the preceding slash (/) can be omitted for the path.

### Short tips

* Be aware that the models are directly set on the component and not on the root view of the component. However, as nested controls automatically inherit the models from their parent controls, the models will be available on the view as well.
* The shell control is now the outermost control of our app and automatically displays a so-called letterbox, if the screen size is larger than a certain width.
* Use data types instead of custom formatters whenever possible.