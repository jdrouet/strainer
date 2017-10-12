# Passoire

[![CircleCI](https://img.shields.io/circleci/project/jdrouet/passoire.svg?maxAge=2592000)](https://circleci.com/gh/jdrouet/passoire)
[![codecov](https://codecov.io/gh/jdrouet/passoire/branch/master/graph/badge.svg)](https://codecov.io/gh/jdrouet/passoire)
![Dependencies](https://david-dm.org/jdrouet/passoire.svg)

# How to use it

```node
const Schema = require('passoire');

const Tag = new Schema({
  id: {},
  label: {},
});

const Account = new Schema({
  id: {},
  password: {views: []},
  firstName: {views: ['public', 'user', 'admin']},
  lastName: {views: ['user', 'admin']},
  email: {views: ['user', 'admin']},
  tags: {array: true, schema: Tag, views: ['user', 'admin']},
});

const account = {
  id: 1,
  password: 'such a funny password',
  firstName: 'Jean',
  lastName: 'Luc',
  email: 'jean-luc@gmail.com',
  tags: [
    {id: 1, label: 'french'},
    {id: 2, label: 'rider'},
  ],
};

console.log(Account.clean(account));
console.log(Account.clean(account, 'public'));
```

Will output
```node
{ id: 1,
  password: 'such a funny password',
  firstName: 'Jean',
  lastName: 'Luc',
  email: 'jean-luc@gmail.com',
  tags: [ { id: 1, label: 'french' }, { id: 2, label: 'rider' } ] }
{ id: 1, firstName: 'Jean' }
```
