// I need to add a handler function when new data are created, when the record is newly created
// A namespace defined for the sample code
// As a best practice, you should always define
// a unique namespace for your libraries
var Example3 = window.Example3 || {};
(function () {
  const secrectText = "helloWorld";
  const secrectNumber = 111;

  this.alertOnLoad = function (executionContext) {
    try {
      // debugger;
      // Get the 'formContext' from 'executionContext':
      const formContext = executionContext.getFormContext();
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
      // Set visibility for 'Timeline tab', you need to define the unique ID name in PowerApss and use it in here:
      let timelineTab = formContext.ui.tabs.get("timeline_tab");
      if (!inspectionRequired) {
        timelineTab.setVisible(false);
      }
      // debugger;
      // Verify "crff8_changeadaptcustom" value equals to secretText, set visible if true:
      if (
        formContext.getAttribute("crff8_changeadaptcustom").getValue() != null
      ) {
        if (
          formContext
            .getAttribute("crff8_changeadaptcustom")
            .getValue()
            .localeCompare(secrectText) == 0
        ) {
          formContext
            .getControl("crff8_displaytempvaluecustom")
            .setVisible(true);
        }
      }

      // Verify "crff8_adaptmultiplecustom" value is true, set visible if true:
      const multipleChoiceValue = formContext
        .getAttribute("crff8_adaptmultiplecustom")
        .getValue();
      if (multipleChoiceValue) {
        formContext
          .getControl("crff8_multiplechoicetestcustom")
          .setVisible(true);
      }
      // debugger;
      // Use `addOnChange` to set a function to be called when an "on change" event occur for a field:
      /* You can totally trigger this using `onChange` from a field but it's safer to trigger this from `onLoad`. */
      // add onChange trigger for "crff8_changeadaptcustom" (text field):
      formContext
        .getAttribute("crff8_changeadaptcustom")
        .addOnChange(this.displayTempFieldOnChange);
      // add onChange trigger for "crff8_adaptmultiplecustom" (multiple choice):
      formContext
        .getAttribute("crff8_adaptmultiplecustom")
        .addOnChange(this.multipleChoiceDisplayOnChange);
      debugger;
      console.log(
        "This is the value the second time: " +
          JSON.stringify(caladanHouse, null, 2)
      );
    } catch (error) {
      debugger;
      console.error(`Error message for "alertOnLoad()": ` + error);
    }
  };
  this.displayTempFieldOnChange = function (executionContext) {
    try {
      debugger;
      const formContext = executionContext.getFormContext();
      const getSecretInput = formContext.getAttribute(
        "crff8_changeadaptcustom"
      );
      let getSecretInputText = getSecretInput.getValue();
      if (getSecretInputText.localeCompare(secrectText) == 0) {
        // if getSecretInputText equals secretText, trigger the easter egg:
        alert("You have found an Easter Egg!");
        formContext.getControl("crff8_displaytempvaluecustom").setVisible(true);
      } else {
        formContext
          .getControl("crff8_displaytempvaluecustom")
          .setVisible(false);
      }
      let getSecretInputNumber =
        Example3.checkAndConvertNumber(getSecretInputText);
      if (getSecretInputNumber == secrectNumber) {
        // if getSecretInputText equals secretNumber, change multiple choice value to true and fire on change:
        const multipleChoiceFieldAttribute = formContext.getAttribute(
          "crff8_adaptmultiplecustom"
        );
        multipleChoiceFieldAttribute.setValue(true);
        multipleChoiceFieldAttribute.setSubmitMode("always");
        /* Normally, changing the multiple choice value using the UI does trigger the onChange event. However, changing the multiple choice's value 
        doesn't trigger the onChange event. For this, you will need fireOnChange().
        More info here: https://chatgpt.com/share/67f4996d-71bc-8010-ad07-6432c4fc865d + https://chatgpt.com/share/67f49d20-e55c-8010-9792-e120560c067c*/
        multipleChoiceFieldAttribute.fireOnChange();
      } else {
        console.log("false case");
        formContext.getAttribute("crff8_adaptmultiplecustom").setValue(false);
        formContext
          .getControl("crff8_multiplechoicetestcustom")
          .setVisible(false);
      }
    } catch (error) {
      debugger;
      console.error(`Error message for "displayTempFieldOnChange()": ` + error);
    }
  };
  this.checkAndConvertNumber = function (input) {
    if (isNaN(input)) {
      return null;
    } else {
      return Number(input);
    }
  };
  this.multipleChoiceDisplayOnChange = function (executionContext) {
    try {
      // debugger;
      const formContext = executionContext.getFormContext();
      let getMultipleChoiceValue = formContext
        .getAttribute("crff8_adaptmultiplecustom")
        .getValue();
      if (getMultipleChoiceValue) {
        formContext
          .getControl("crff8_multiplechoicetestcustom")
          .setVisible(true);
      } else {
        formContext
          .getControl("crff8_multiplechoicetestcustom")
          .setVisible(false);
      }
    } catch (error) {
      debugger;
      console.error(
        `Error message for "multipleChoiceDisplayOnChange()": ` + error
      );
    }
  };
}).call(Example3);
