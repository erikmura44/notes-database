# app with database

- mkdir
- cd into dir
- npm init -y
- npm install --save pg knex
- knex init

### knexfile.js UPDATE
```javascript
module.exports = {

  development: {
    client: 'pg',
    connection: 'postgres://localhost/music'
  },

  production: {
    client: 'pg',
    connection: process.env.DATABASE_URL
  }

}
```
then create migrations:

knex migrate:make <name>

then inside that migration:
```javascript
exports.up = function(knex, Promise) {
  return knex.schema.createTable("artist", function (table) {
    table.increments()
    table.text("name")
  })
}

exports.down = function(knex, Promise) {
  return knex.schema.dropTable("artist")
}
```

knex migrate:latest

createdb <db name>

knex migrate:latest

git init...

then make seeds

knex seed:make <name>
```javascript
exports.seed = function(knex, Promise) {
  return Promise.join(
    // Deletes ALL existing entries
    knex('artist').del(),

    // Inserts seed entries
    knex('artist').insert({id: 1, name: 'The Beatles'}),
    knex('artist').insert({id: 2, name: 'The Flaming Lips'})
  );
};
```

knex seed:run
