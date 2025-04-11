var RTExample = window.RTExample || {};
(function () {
  this.buttonOnClick = async function (primaryControl) {
    try {
      const formContext = primaryControl;
      const getRecordNumID = formContext.getAttribute("crff8_name").getValue();

      const envVarDefSchemaName = "crff8_MyEnvVar";
      const envVarGUID = await this.getEnvVarGUID(envVarDefSchemaName);
      if (envVarGUID) {
        const envVarVal = await this.getEnvVarValue(envVarGUID);
        // console.log("Record Number ID is: " + getRecordNumID);
        // console.log(envVarGUID);
        // console.log(envVarVal);
        alert(
          `Record Number ID: ${getRecordNumID}\nEnvVar GUID: ${envVarGUID}\nEnvVar Value: ${envVarVal}\n------------`
        );
      } else {
        console.log("Get EnvVarGUID is Empty!");
      }
    } catch (error) {
      debugger;
      console.error("RTExample Error: " + error.message);
    }
  };
  this.getEnvVarGUID = async function (schemaName) {
    try {
      const envVarDefTable = "environmentvariabledefinition";
      const envVarDefColumns =
        "schemaname,environmentvariabledefinitionid,createdon";
      const query = `?$filter=schemaname eq '${schemaName}'&$select=${envVarDefColumns}`;
      // const query = `?$filter=schemaname eq 'crff8_MyEnvVar'&$select=schemaname,environmentvariabledefinitionid,createdon`;
      const result = await Xrm.WebApi.retrieveMultipleRecords(
        envVarDefTable,
        query
      );
      if (result.entities.length > 0) {
        // receive 3 columns being schema name, environmentvariabledefinitionid and createdon
        return result.entities[0].environmentvariabledefinitionid; // choose environmentvariabledefinitionid only for return
      } else {
        return null;
      }
    } catch (error) {
      debugger;
      console.error("Get Env Var GUID Error: " + error.message);
    }
  };
  this.getEnvVarValue = async function (GUID) {
    try {
      const envVarValTable = "environmentvariablevalue";
      const envVarValColumns = "schemaname,value";
      const query = `?$filter=_environmentvariabledefinitionid_value eq '${GUID}'&$select=${envVarValColumns}`;
      const result = await Xrm.WebApi.retrieveMultipleRecords(
        envVarValTable,
        query
      );
      if (result.entities.length > 0) {
        return result.entities[0].value;
      } else {
        return null;
      }
    } catch (error) {
      debugger;
      console.error("Get Env Var Value Error: " + error.message);
    }
  };
}).call(RTExample);
