### Webhook

1. Click `+` and search **Webhook** and click on it.
2. Change the HTTP Method to: `PUT`
3. Change the path field to: `update`

### Edit Fields

1. Click `+`
2. Search **Edit Fields** - click on it.
3. Change to: `Set Add Fields`

#### Fields:

- **id**: `{{ $json["body"]["id"] }}`
- **title**: `{{ $json["body"]["title"] }}`
- **description**: `{{ $json["body"]["description"] }}`
- **status**: `{{ $json["body"]["status"] }}`

### Code Node

1. Click `+`
2. Search for **Code** and click on it.

Here is the prompt to enter in the code AI field:

```
Generate JavaScript code that extracts and handles data from a node's 'Edit Fields' output. The code should check if the 'Edit Fields' node exists and has a 'json' property. If the data exists, it should be logged, and if not, an error should be thrown. Then, extract the 'id', 'title', 'description', and 'status' fields from the node's data. Log the 'title' and 'description' values, and finally, return a new object containing the 'id', 'title', 'description', and 'status' as 'json' format.
```

### Google Sheets

1. Click **+** and search **Google Sheets**.
2. Select **Update row in sheet**.
3. Select your **Document** (Google spreadsheet).
4. Select your **Sheet** (Tab).

Drag and drop fields from the **INPUT code** to the correct fields.
(Go back to Postman and send the update request if you haven't already done so. You will need to Click the Test workflow button on the Canvas before you can send a request. Then in the Google sheet click the Test step button.)

### Postman

1. Create a request with **PUT** and paste the URL from the Webhook.
2. Click **Body** then select **raw** and **JSON**.
3. Enter this text:
   ```json
   {
     "id": 3,
     "title": "Todo 3 update",
     "description": "description updaded",
     "status": "Completed"
   }
   ```
