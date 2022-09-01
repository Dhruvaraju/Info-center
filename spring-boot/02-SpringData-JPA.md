## SpringData JPA
#springdata #jpa

### Querying using sub object attributes
When we have an entity with sub entities we can query them by using the `_` notation.
Example: User entity has a Address Sub entity with zipCode as attribute

```
//User
User {
String name;
Address address;
}

//Address
Address{
String place;
String zipCode;
}
```

- We can query User entity based on Zipcode like
- `findByAddress_Zipcode(String zipcode)`
- We can also do a contains query as 
- `findByAddress_PlaceContains(String place)`