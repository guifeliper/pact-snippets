# Basic Pact Snippets

A collection of Pact snippets and commands. 

![snippets in action](images/snippets-in-action.gif)
## Snippets

| Snippet | Renders                                       |
| ------- | --------------------------------------------- |
| `defun` | Create a function                                 |
| `module`| Create a module                      |
| `defschema`| Create a schema                      |
| `deftable`| Create a table                      |
| `pacthello`| Generate an example of hello                     |
| `define-keyset`| Create a basic define-keyset template                     |
| `enforce-keyset`| Create a basic enforce-keyset template                    |
| `read-keyset`| Create a basic read-keyset template                    |
| `keys-2`| Create a keys-2 template                     |
| `keys-all`| Create a keys-all template                   |
| `keys-any`| Create a keys-any template                   |
| `emit-event`| Create a emit-event template                 |
| `enforce-guard`| Create a enforce-guard template                   |
| `install-capability`| Create a basic install-capability template                 |
| `with-capability`| Create a basic install-capability template                |


## Full Expansions

### defun - Create a function

```
(defun | (|)
    @doc " | "
|)
```

### module - Create a module
```
(module | '|
  @doc " | "
|)
```

### defschema - Create a schema
```
 (defschema 
   @doc " "
 foo:bar)
```

### deftable - Create a table  
```
(deftable foo:{bar})
```

### pacthello - Generate an example of hello 
```
(namespace "free")
;;---------------------------------
;;
;;  Create an 'admin-keyset' and add some key, for loading this contract!
;;
;;  Make sure the message is signed with this added key as well.
;;
;;  When deploying new contracts, ensure to use a *unique keyset name*
;;  and *unique module name* from any previously deployed contract
;;
;;
;;---------------------------------
 
 
;; Keysets cannot be created in code, thus we read them in
;; from the load message data.
(define-keyset "free.admin-keyset" (read-keyset "admin-keyset"))
;; Define the module. The module name must be unique
(module hello-world GOV
  "A smart contract to greet the world."
 
;; Define module governance function
(defcap GOV ()
   (enforce-keyset "free.admin-keyset"))
(defun hello (name:string)
 "Do the hello-world dance"
 (format "Hello {}!" [name]))
)
 
;; and say hello!
(hello "world")
```

### define-keyset - Create a basic define-keyset template
```
(define-keyset '|foo-keyset (read-keyset "|bar"))
```

### enforce-keyset - Create a basic enforce-keyset template
```
(enforce-keyset '|foo-keyset)
```


### read-keyset - Create a basic read-keyset template
```
(read-keyset "|foo-keyset")
```

### keys-2 - Create a basic keys-2 template
```
(keys-2 |3 |1)
```

### keys-any - Create a basic keys-any template
```
(keys-any |10 |1)
```

### keys-all - Create a basic keys-all template
```
(keys-all |3 |3)
```

### emit-event - Create a basic emit-event template
```
(emit-event (TRANSFER "|Bob" "|Alice" |12.0))
```

### enforce-guard - Create a basic enforce-guard template
```
(enforce-guard |row-guard)
```

### install-capability - Create a basic install-capability template
```
(install-capability (PAY "|alice" "|bob" |10.0))
```


### with-capability - Create a basic with-capability template
```
(with-capability (|UPDATE-USERS |id) (|update users id { salary: new-salary }))
```