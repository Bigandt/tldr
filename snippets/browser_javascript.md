# Browser javascript snippets

## jquery modal dialog with textarea

```
// Load jquery first (also stylesheet)
(function() {
    // Load the script 1
    var script = document.createElement("SCRIPT");
    script.src = 'https://code.jquery.com/jquery-1.11.1.min.js';
    script.type = 'text/javascript';
    document.getElementsByTagName("head")[0].appendChild(script);

    // Load the script 2
    script = document.createElement("SCRIPT");
    script.src = 'https://code.jquery.com/ui/1.11.1/jquery-ui.min.js';
    script.type = 'text/javascript';
    document.getElementsByTagName("head")[0].appendChild(script);
})();

// Wait for load

$('head').append('<link rel="stylesheet" type="text/css" href="https://code.jquery.com/ui/1.11.1/themes/smoothness/jquery-ui.css">');

// Wait for load

// modal
$('<div></div>').dialog({
    modal: true,
    width: 800,
	height: 410,
	resizable: false,
	dialogClass: 'ui-dialog--notification ui-dialog',
    open: function() {
      var markup = '<div><p>Some text ...<br><br>Do you wish to proceed?</p></div><textarea id="myTextAreaID" rows="11" cols="50" maxlength="500" style="resize: none; border: none; outline: none;">' + defaultText  + '</textarea>';
      $(this).html(markup);
    },
	buttons: [
				{
				   text: "Cancel",
				   "class": 'ui-button ui-corner-all ui-widget',
				   click: function() { 
					  $(this).dialog("close"); 
				   }
				},
				{
				   text: "OK",
				   "class": 'js-confirmBtn ui-button ui-corner-all ui-widget ui-button--hot',
				   click: function() {    
					  // OK function call here
					  $(this).dialog("close"); 
				   }
				}
			  ]
});  //end confirm dialog
```

