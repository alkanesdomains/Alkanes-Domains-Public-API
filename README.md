# Alkanes-Domains-Public-API

#  Alkanes Domains API

The Alkanes Domains API allows you to query domain ownership details on the Bitcoin blockchain using the `.btc` namespace. Below is documentation for the `/api/domain-holder` endpoint, which returns the wallet address of a primary `.btc` domain.

---

## 🔍 Get Domain Holder

Returns the **holder wallet address** of a `.btc` domain **only if** it is marked as **primary** in the database.

### 📮 Endpoint

POST https://alkanes.domains/api/domain-holder

---

## 📤 Request Body

Send a JSON payload containing the domain name. The name **must end with `.btc`**:

{
  "name": "example.btc"
}

---

## ✅ Success Response

If the domain exists and is set as primary, you’ll receive:

{
  "success": true,
  "holder": "bc1pabc123..."
}

---

## ❌ Error Responses

### 1. Missing `name` Field

{
  "error": "Domain name is required"
}

### 2. Invalid Suffix (Not `.btc`)

{
  "success": false,
  "error": "Domain name must end with .btc"
}

### 3. Domain Not Found or Not Primary

{
  "success": false,
  "message": "Domain not found or not primary"
}

### 4. Internal Server Error

{
  "error": "Internal server error"
}

---

## 🧪 Example Usage

Use `curl` to query a domain:

curl -X POST https://alkanes.domains/api/domain-holder \
  -H "Content-Type: application/json" \
  -d '{"name": "example.btc"}'

---

## ℹ️ Notes

- The domain **must be minted** and explicitly **marked as primary** in the Alkanes system.
- Only `.btc` domains are supported.
- Response includes the **Taproot or SegWit address** of the domain holder if applicable.

---
