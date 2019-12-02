# zpl-rest
zpl-rest provides the following
- REST-API to manage labels (written in ZPL), Printer and to print these Printers with these labels
- a simple graphical user interface for this REST-API
- you can use placeholder in your ZPL labels (${varname}) which will be replaced through the API e.g.:
```ZPL
^XA
^LH0,0
^MTT
^A0N,36,36
^FO236,71
^FD${sometext}^FS
^XZ
```

which you can replace with the following POST-request to `/rest/print`:
```JSON
{
    printer:"printer id",
    label:"id of the label",
    data : {
      sometext: "hello world"
    }
}
```
## installation and start

download this repo und run `npm start`

## frontend
![a screenshot of the frontend](https://github.com/mrothenbuecher/zpl-rest/raw/master/img/screenshot.png "screenshot")

## REST-API

| Method              | Path                | parameter                                                                           | description                         |
| ------------------- | ------------------- | ----------------------------------------------------------------------------------- | ----------------------------------- |
| get                 | /rest/printer       | none                                                                                | list of all printers                |
| get                 | /rest/label         | none                                                                                | list of all labels                  |
| get                 | /rest/jobs          | none                                                                                | list of all printjobs               |
| post                | /rest/print         | {printer:"printer_id...",label:"label_id...", data: {...}}                          | actual print                        |
| post                | /rest/printer       | to add : {address:"..",name:"..."} for update {_id:"...",address:"..",name:"..."}   | add or update a printer             |
| post                | /rest/label         | to add : {name:"..."} for update {_id:"...",name:"..."}                             | add or update a label               |
| delete              | /rest/printer/(:id) | none                                                                                | removes a printer with the given id |
| delete              | /rest/label/(:id)   | none                                                                                | removes a label with the given id   |

## options

| Option              | Type          | description                                    |  Default  |
| ------------------- |:-------------:| ---------------------------------------------- | :-------: |
| port                | int           | port for the RESTAPI                           |    8000   |
| websocket_port      | int           | websocket port for the frontend                |    8001   |
| public              | bool          | if `false` server only reachable for localhost |     true  |
| secret              | string        | the session secret                             |           |

# thanks to
[template for the frontend](https://startbootstrap.com/themes/sb-admin-2/)