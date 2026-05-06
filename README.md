# Issue: Implement JSON Deep Merge Module with Main File Precedence

**Labels:** `interview-exercise` `code-review` `module`

---

## Summary

Create a function that merges two dictionaries using a precedence-based strategy with this signature: 

```python
def merge_json(main_dict: dict, incoming_dict: dict) -> dict:
  ...
```

A designated `main_dict` dictionary acts as the authoritative source — its existing values are never overwritten. A second `incoming_dict` dictionary provides supplemental data that fills in missing keys only.

---


### Merge Behavior

1. **Top-level keys that exist only in `main_dict`** → preserved as-is.
2. **Top-level keys that exist only in the `incoming_dict`** → added to the merged result.
3. **Top-level keys that exist in both dictionaries:**
   - If the value in `main_dict` is **already populated** (non-null, non-empty), it takes precedence and must **not** be overwritten.
   - If the value in `main_dict` is `None`, `""`, `{}`, or `[]` (empty/unset), the incoming value may fill it in.
4. **Nested objects (recursive merge):**
   - When both dictionaries have an object at the same key, the merge should recurse into the nested structure and apply the same precedence rules at every level.
   - `main_dict` values always win at any depth if they are populated.
5. **Arrays:**
   - If `main_dict` has a non-empty array at a given key, it is preserved entirely (no element-level merge).
   - If `main_dict` has an empty array and the incoming file has a non-empty one, the incoming array is used.

---

## Sample code

Code for use during the technical interview
```python




def merge_json(main_dict: dict, incoming_dict: dict) -> dict:
  pass

### Example 1 ###

ex1_main = {
    "name": "Acme Corp",
    "address": {
      "street": "123 Main St",
      "city": "",
      "state": "WA"
    },
    "tags": ["enterprise"],
    "metadata": {
      "created_by": "admin",
      "notes": None
    },
    "contacts": []
  }

ex1_incoming = {
    "name": "Acme Corporation",
    "address": {
      "street": "456 Oak Ave",
      "city": "Redmond",
      "state": "ME",
      "zip": "98101"
    },
    "tags": ["startup", "west-coast"],
    "metadata": {
      "created_by": "import-script",
      "notes": "Imported from CRM",
      "source": "crm-v2"
    },
    "contacts": [
      { "email": "info@acme.com" }
    ],
    "industry": "Technology"
  }

ex1_result = {
    "name": "Acme Corp",
    "address": {
      "street": "123 Main St",
      "city": "Redmond",
      "state": "WA",
      "zip": "98101"
    },
    "tags": ["enterprise"],
    "metadata": {
      "created_by": "admin",
      "notes": "Imported from CRM",
      "source": "crm-v2"
    },
    "contacts": [
      { "email": "info@acme.com" }
    ],
    "industry": "Technology"
  }

### Example 2 ###

ex2_main = {
    "user": "jdoe",
    "profile": {
      "bio": "",
      "links": ["https://jdoe.dev"]
    },
    "active": True
  }

ex2_incoming = {
    "user": "john.doe",
    "profile": {
      "bio": "Engineer based in Seattle.",
      "links": ["https://example.com"],
      "avatar": "avatar.png"
    },
    "role": "admin"
  }

ex2_result = {
    "user": "jdoe",
    "profile": {
      "bio": "Engineer based in Seattle.",
      "links": ["https://jdoe.dev"],
      "avatar": "avatar.png"
    },
    "active": True,
    "role": "admin"
  }

### Example 3 ###

ex3_main = {
  "settings": {
    "theme": "dark",
    "notifications": {}
  },
  "tags": []
}

ex3_incoming = {
  "settings": {
    "theme": "light",
    "notifications": {
      "email": True,
      "sms": false
    }
  },
  "tags": ["beta", "internal"]
}

ex3_result = {
    "settings": {
      "theme": "dark",
      "notifications": {
        "email": True,
        "sms": false
      }
    },
    "tags": ["beta", "internal"]
  }
```

---
