### Webhook

1. Remove exist node and click `+`
2. Search **Webhook** and click on it.
3. Change the HTTP Method to: `POST`
4. Change the path field to: `add`

### Edit Fields

1. Click `+`
2. Search **Edit Fields** - click on it.
3. Change to: `Set Add Fields`

#### Fields:

- **id**: `{{ $json["body"]["id"] ? $json["body"]["id"] : null }}`
- **title**: `{{ $json["body"]["title"] }}`
- **description**: `{{ $json["body"]["description"] }}`

### Get rows

1. Click `+` and search **Google Sheets**
2. Click **Get row(s) in Sheet**
3. Change to: `Get Add Rows`
4. Select your Document (Google spreadsheet)
5. Select your Sheet (Tab)
6. Next, go to the **Settings** tab
7. Toggle **Always Output Data** on
8. In the **On Error** select "Continue"

### Code Node

1. Click `+`
2. Search for **Code** and click on it.

Here is the code to enter in the code field:

```javascript
// Access data from the input (Get Add Rows node)
const data = $input.all();

console.log('Data from Get Add Rows:', data);

// Extract and parse existing IDs
const ids = data
  .map((item) => parseInt(item.json['ID'], 10))
  .filter((id) => !isNaN(id));
console.log('Extracted IDs:', ids);

// Calculate the next ID
const nextId = ids.length > 0 ? Math.max(...ids) + 1 : 1;
console.log('Next ID:', nextId);

// Access data from 'Set Add Fields' node (assuming it's executed before and data is available)
let editFieldsData = null;
if ($node['Set Add Fields'] && $node['Set Add Fields'].json) {
  editFieldsData = $node['Set Add Fields'].json;
}

console.log('Set Add Fields data:', editFieldsData);

if (!editFieldsData) {
  throw new Error('Set Add Fields node output is undefined or empty.');
}

const title = editFieldsData['title'];
const description = editFieldsData['description'];

console.log('Title:', title);
console.log('Description:', description);

// Return the new item
return [
  {
    json: {
      id: nextId,
      title: title,
      description: description,
      status: 'Active',
    },
  },
];
```

### Google Sheets

1. Click **+** and search **Google Sheets**.
2. Select **Append row in sheet**.
3. Select your **Document** (Google spreadsheet).
4. Select your **Sheet** (Tab).

Drag and drop fields from the **INPUT code** to the correct fields.

### Postman

1. Create a request with **POST** and paste the URL from the Webhook.
2. Click **Body** then select **raw** and **JSON**.
3. Enter this text:
   ```json
   {
     "title": "Todo 1",
     "description": "Test description"
   }
   ```

```

```
