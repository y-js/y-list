
# List Type for Yjs

Manage list-like data with this shareable list type. You can insert and delete arbitrary objects (also custom types for Yjs) in the list type.

## Use it!
Retrieve this with bower or npm.

##### Bower
```
bower install y-list --save
```

and include the js library.

```
<script src="./bower_components/y-list/y-list.js"></script>
```

##### NPM
```
npm install y-list --save
```
and put it on the `Y` object.

```
Y.List = require("y-list");
```


### List Object

##### Reference
* Create
```
var ylist = new Y.List()
```
* .insert(position, content)
  * Insert content at a position
* .insertContents(position, contents)
  * Insert a set of content at a position. This expects that contents is an array of content.
* .push(content)
  * Insert content at the end of the list
* .delete(position, length)
  * Delete content. The *length* parameter is optional and defaults to 1
* .val()
  * Retrieve all content as an Array Object
* .val(position)
  * Retrieve content from a position
* .observe(f)
  * The observer is called whenever something on this list changed. (throws insert, and delete events)
* .unobserve(f)
  * Delete an observer


# A note on consistency
If two users insert something at the same position concurrently, the content that was inserted by the user with the higher user-id will be to the right of the other content. In the OT world we often speak of *intention preservation*, which is very loosely defined in most types. This type has the following notion of intention preservation: When a user inserts content *c* after a set of content *C_left*, and before a set of content *C_right*, then *C_left* will be always to the left of c, and *C_right* will be always to the right of *c*. This property will also hold when content is deleted or when a deletion is undone.

# A note on time properties
* .insert(position, content)
  * O(position)
* .insertContents(position, contents)
  * O(position + |contents|)
* .push(content)
  * O(1)
* .delete(position, length)
  * O(position)
* .val()
  * O(|ylist|)
* .val(position)
  * O(position|)
* Appy a delete operation from another user
  * O(1)
* Appy an insert operation from another user
  * Yjs does not transform against operations that do not conflict with each other.
  * An operation conflicts with another operation if it intends to be inserted at the same position.
  * Overall worst case complexety: O(|conflicts|!)


# Issues
* Support moving of objects
* Create a polymer element

## License
Yjs is licensed under the [MIT License](./LICENSE.txt).

<kevin.jahns@rwth-aachen.de>