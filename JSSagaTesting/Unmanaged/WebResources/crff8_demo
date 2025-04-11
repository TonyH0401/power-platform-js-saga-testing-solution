// A namespace defined for the sample code
// As a best practice, you should always define
// a unique namespace for your libraries
var Example = window.Example || {};
(function () {
  const secrectText = "helloWorld";

  this.alertOnLoad = function (executionContext) {
    try {
      // debugger;
      // Get the 'formContext' from 'executionContext':
      let formContext = executionContext.getFormContext();
      // debugger;
      // Get values from attributes:
      let houseAddress =
        formContext
          .getAttribute("crff8_caladanhouseaddresscustom")
          .getValue() || "default address";
      let yearBuilt =
        formContext.getAttribute("crff8_yearbuilt").getValue() ||
        "default year built";
      let inspectionRequired = formContext
        .getAttribute("crff8_caladanhouseinspectionrequiredcustom")
        .getValue();
      inspectionRequired =
        inspectionRequired === undefined ? null : inspectionRequired;
      let inspectionDate = "";
      if (inspectionRequired) {
        inspectionDate = formContext
          .getAttribute("crff8_inspectiondatecustom")
          .getValue();
      }
      // debugger;
      // Define object with values:
      const caladanHouse = {
        houseAddress: houseAddress,
        yearBuilt: new Date(yearBuilt).toLocaleDateString(),
        inspectionRequired: inspectionRequired,
        ...(inspectionDate
          ? { inspectionDate: new Date(inspectionDate).toLocaleDateString() }
          : {}),
      };
      // debugger;
      // Set visibility for 'Timeline tab':
      let timelineTab = formContext.ui.tabs.get("timeline_tab");
      if (!inspectionRequired) {
        timelineTab.setVisible(false);
      }
      // debugger;
      // Check easter egg exists onLoad:
      if (
        formContext
          .getAttribute("crff8_changeadaptcustom")
          .getValue()
          .localeCompare(secrectText) == 0
      ) {
        formContext.getControl("crff8_displaytempvaluecustom").setVisible(true);
      }
      // debugger;
      // Use `addOnChange` to set a function to be called when an "on change" event occur for a field:
      /* You can totally trigger this using `onChange` from a field but it's safer to trigger this from `onLoad`. */
      formContext
        .getAttribute("crff8_changeadaptcustom")
        .addOnChange(this.displayTempFieldOnChange);
      debugger;
      console.log(
        "This is the value: " + JSON.stringify(caladanHouse, null, 2)
      );
    } catch (error) {
      debugger;
      console.error(`Error message for "alertOnLoad()": ` + error);
    }
  };
  this.displayTempFieldOnChange = function (executionContext) {
    try {
      debugger;
      let formContext = executionContext.getFormContext();
      let getSecretInputText = formContext
        .getAttribute("crff8_changeadaptcustom")
        .getValue();
      if (getSecretInputText.localeCompare(secrectText) == 0) {
        alert("You have found an Easter Egg!");
        formContext.getControl("crff8_displaytempvaluecustom").setVisible(true);
      } else {
        formContext
          .getControl("crff8_displaytempvaluecustom")
          .setVisible(false);
      }
    } catch (error) {
      debugger;
      console.error(`Error message for "displayTempFieldOnChange()": ` + error);
    }
  };
}).call(Example);
