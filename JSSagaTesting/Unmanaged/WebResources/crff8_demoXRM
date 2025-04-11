// I need to add a handler function when new data are created, when the record is newly created
// A namespace defined for the sample code
// As a best practice, you should always define
// a unique namespace for your libraries
var ExampleXRM = window.ExampleXRM || {};
(function () {
  this.alertOnLoad = async function (executionContext) {
    try {
      // debugger;
      // Get the 'formContext' from 'executionContext':
      const formContext = executionContext.getFormContext();
      const rawHouseGUID = formContext.data.entity.getId();
      if (
        !rawHouseGUID ||
        rawHouseGUID === "00000000-0000-0000-0000-000000000000"
      ) {
        console.warn(
          "House GUID not available yet (record is probably unsaved)."
        );
        const generalTab = formContext.ui.tabs.get("tab_general");
        const section = generalTab.sections.get("null_section_3");
        section.setVisible(false);
        return;
      }
      const formattedHouseGUID = rawHouseGUID.replace("{", "").replace("}", "");
      debugger;
      // console.log(`Raw House GUID: ${rawHouseGUID}`);
      // console.log(`Formatted House GUID: ${formattedHouseGUID}`);

      const furnitureNumber = await this.getHouseFurnitures(formattedHouseGUID);
      if (furnitureNumber == 0) {
        const generalTab = formContext.ui.tabs.get("tab_general");
        const section = generalTab.sections.get("null_section_3");
        section.setVisible(false);
      }
    } catch (error) {
      debugger;
      console.error(`Error message for "alertOnLoad()": ` + error);
    }
  };
  this.getHouseFurnitures = async function (houseGUID) {
    try {
      const furnitureTable = "crff8_caladanfurniture"; // 703797B4-1B11-F011-998A-000D3AA12CF4
      // For more information: https://learn.microsoft.com/en-us/power-apps/developer/data-platform/webapi/query/select-columns#lookup-property-data.
      const furnitureHouseLookup = "_crff8_caladanhouselookup_value";
      const furnitureColumns = "crff8_name,crff8_furniturenamecustom";
      // ?$filter=_crff8_caladanhouselookup_value eq 703797B4-1B11-F011-998A-000D3AA12CF4&$select=crff8_name
      const query = `?$filter=${furnitureHouseLookup} eq ${houseGUID}&$select=${furnitureColumns}`;
      const result = await Xrm.WebApi.retrieveMultipleRecords(
        furnitureTable,
        query
      );
      // console.log(`Fetched ${result.entities.length} furniture records:`);
      return result.entities.length;
    } catch (error) {
      debugger;
      console.error("GetHouseFurnitures Error:", error.message);
    }
  };
}).call(ExampleXRM);
