# solid1-pouchdb-collection
Solid-js v1 store for PouchDB collections.

# Usage
```typescript
// solid-component.tsx
import {use_collection} from "solid1-pouchdb-collection";
import PouchDB from "pouchdb-browser";

interface Customer {
  name: string;
  trusted: boolean;
}
const customers_db = new PouchDB<Customer>();

function Component() {
const [customers, upsertCustomer, removeCustomer] = use_collection(db_customers);

  function trust(customer) {
    return async function onclick() {
      try {
        await upsertCustomer({ ...customer, trusted: true });
        alert("Success!");
      } catch (err) {
        console.error(err);
      }
    };
  }

  function remove(customer) {
    return async function onclick() {
      try {
        await removeCustomer(customer);
        alert("Success!");
      } catch (err) {
        console.error(err);
      }
    };
  }

  return customers.map(function map(customer) {
    return (
      <div>
        <p>{customer.name}</p>
        <button onclick={trust(customer)}>Trust</button>
        <button onclick={remove(customer)}>Remove</button>
      </div>
    );
  });
}
```
