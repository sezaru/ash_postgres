<!--
This file was generated by Spark. Do not edit it by hand.
-->
# DSL: AshPostgres.DataLayer

A postgres data layer that leverages Ecto's postgres capabilities.


## postgres
Postgres data layer configuration


### Nested DSLs
 * [custom_indexes](#postgres-custom_indexes)
   * index
 * [custom_statements](#postgres-custom_statements)
   * statement
 * [manage_tenant](#postgres-manage_tenant)
 * [references](#postgres-references)
   * reference
 * [check_constraints](#postgres-check_constraints)
   * check_constraint


### Examples
```
postgres do
  repo MyApp.Repo
  table "organizations"
end

```




### Options

| Name | Type | Default | Docs |
|------|------|---------|------|
| [`repo`](#postgres-repo){: #postgres-repo .spark-required} | `module \| (any, any -> any)` |  | The repo that will be used to fetch your data. See the `AshPostgres.Repo` documentation for more. Can also be a function that takes a resource and a type `:read \| :mutate` and returns the repo |
| [`migrate?`](#postgres-migrate?){: #postgres-migrate? } | `boolean` | `true` | Whether or not to include this resource in the generated migrations with `mix ash.generate_migrations` |
| [`migration_types`](#postgres-migration_types){: #postgres-migration_types } | `keyword` | `[]` | A keyword list of attribute names to the ecto migration type that should be used for that attribute. Only necessary if you need to override the defaults. |
| [`migration_defaults`](#postgres-migration_defaults){: #postgres-migration_defaults } | `keyword` | `[]` | A keyword list of attribute names to the ecto migration default that should be used for that attribute. The string you use will be placed verbatim in the migration. Use fragments like `fragment(\\"now()\\")`, or for `nil`, use `\\"nil\\"`. |
| [`base_filter_sql`](#postgres-base_filter_sql){: #postgres-base_filter_sql } | `String.t` |  | A raw sql version of the base_filter, e.g `representative = true`. Required if trying to create a unique constraint on a resource with a base_filter |
| [`simple_join_first_aggregates`](#postgres-simple_join_first_aggregates){: #postgres-simple_join_first_aggregates } | `list(atom)` | `[]` | A list of `:first` type aggregate names that can be joined to using a simple join.  Use when you have a `:first` aggregate that uses a to-many relationship , but your `filter` statement ensures that there is only one result. Optimizes the generated query. |
| [`skip_unique_indexes`](#postgres-skip_unique_indexes){: #postgres-skip_unique_indexes } | `atom \| list(atom)` | `false` | Skip generating unique indexes when generating migrations |
| [`unique_index_names`](#postgres-unique_index_names){: #postgres-unique_index_names } | `list({list(atom), String.t} \| {list(atom), String.t, String.t})` | `[]` | A list of unique index names that could raise errors that are not configured in identities, or an mfa to a function that takes a changeset and returns the list. In the format `{[:affected, :keys], "name_of_constraint"}` or `{[:affected, :keys], "name_of_constraint", "custom error message"}` |
| [`exclusion_constraint_names`](#postgres-exclusion_constraint_names){: #postgres-exclusion_constraint_names } | `any` | `[]` | A list of exclusion constraint names that could raise errors. Must be in the format `{:affected_key, "name_of_constraint"}` or `{:affected_key, "name_of_constraint", "custom error message"}` |
| [`identity_index_names`](#postgres-identity_index_names){: #postgres-identity_index_names } | `any` | `[]` | A keyword list of identity names to the unique index name that they should use when being managed by the migration generator. |
| [`foreign_key_names`](#postgres-foreign_key_names){: #postgres-foreign_key_names } | `list({atom \| String.t, String.t} \| {atom \| String.t, String.t, String.t})` | `[]` | A list of foreign keys that could raise errors, or an mfa to a function that takes a changeset and returns a list. In the format: `{:key, "name_of_constraint"}` or `{:key, "name_of_constraint", "custom error message"}` |
| [`migration_ignore_attributes`](#postgres-migration_ignore_attributes){: #postgres-migration_ignore_attributes } | `list(atom)` | `[]` | A list of attributes that will be ignored when generating migrations. |
| [`table`](#postgres-table){: #postgres-table } | `String.t` |  | The table to store and read the resource from. If this is changed, the migration generator will not remove the old table. |
| [`schema`](#postgres-schema){: #postgres-schema } | `String.t` |  | The schema that the table is located in. Schema-based multitenancy will supercede this option. If this is changed, the migration generator will not remove the old schema. |
| [`polymorphic?`](#postgres-polymorphic?){: #postgres-polymorphic? } | `boolean` | `false` | Declares this resource as polymorphic. See the [polymorphic resources guide](/documentation/topics/polymorphic_resources.md) for more. |


## postgres.custom_indexes
A section for configuring indexes to be created by the migration generator.

In general, prefer to use `identities` for simple unique constraints. This is a tool to allow
for declaring more complex indexes.


### Nested DSLs
 * [index](#postgres-custom_indexes-index)


### Examples
```
custom_indexes do
  index [:column1, :column2], unique: true, where: "thing = TRUE"
end

```




## postgres.custom_indexes.index
```elixir
index fields
```


Add an index to be managed by the migration generator.




### Examples
```
index ["column", "column2"], unique: true, where: "thing = TRUE"
```



### Arguments

| Name | Type | Default | Docs |
|------|------|---------|------|
| [`fields`](#postgres-custom_indexes-index-fields){: #postgres-custom_indexes-index-fields } | `atom \| String.t \| list(atom \| String.t)` |  | The fields to include in the index. |
### Options

| Name | Type | Default | Docs |
|------|------|---------|------|
| [`error_fields`](#postgres-custom_indexes-index-error_fields){: #postgres-custom_indexes-index-error_fields } | `list(atom)` |  | The fields to attach the error to. |
| [`name`](#postgres-custom_indexes-index-name){: #postgres-custom_indexes-index-name } | `String.t` |  | the name of the index. Defaults to "#{table}_#{column}_index". |
| [`unique`](#postgres-custom_indexes-index-unique){: #postgres-custom_indexes-index-unique } | `boolean` | `false` | indicates whether the index should be unique. |
| [`concurrently`](#postgres-custom_indexes-index-concurrently){: #postgres-custom_indexes-index-concurrently } | `boolean` | `false` | indicates whether the index should be created/dropped concurrently. |
| [`using`](#postgres-custom_indexes-index-using){: #postgres-custom_indexes-index-using } | `String.t` |  | configures the index type. |
| [`prefix`](#postgres-custom_indexes-index-prefix){: #postgres-custom_indexes-index-prefix } | `String.t` |  | specify an optional prefix for the index. |
| [`where`](#postgres-custom_indexes-index-where){: #postgres-custom_indexes-index-where } | `String.t` |  | specify conditions for a partial index. |
| [`message`](#postgres-custom_indexes-index-message){: #postgres-custom_indexes-index-message } | `String.t` |  | A custom message to use for unique indexes that have been violated |
| [`include`](#postgres-custom_indexes-index-include){: #postgres-custom_indexes-index-include } | `list(String.t)` |  | specify fields for a covering index. This is not supported by all databases. For more information on PostgreSQL support, please read the official docs. |
| [`all_tenants?`](#postgres-custom_indexes-index-all_tenants?){: #postgres-custom_indexes-index-all_tenants? } | `boolean` | `false` | Whether or not the index should factor in the multitenancy attribute or not. |





### Introspection

Target: `AshPostgres.CustomIndex`


## postgres.custom_statements
A section for configuring custom statements to be added to migrations.

Changing custom statements may require manual intervention, because Ash can't determine what order they should run
in (i.e if they depend on table structure that you've added, or vice versa). As such, any `down` statements we run
for custom statements happen first, and any `up` statements happen last.

Additionally, when changing a custom statement, we must make some assumptions, i.e that we should migrate
the old structure down using the previously configured `down` and recreate it.

This may not be desired, and so what you may end up doing is simply modifying the old migration and deleting whatever was
generated by the migration generator. As always: read your migrations after generating them!


### Nested DSLs
 * [statement](#postgres-custom_statements-statement)


### Examples
```
custom_statements do
  # the name is used to detect if you remove or modify the statement
  statement :pgweb_idx do
    up "CREATE INDEX pgweb_idx ON pgweb USING GIN (to_tsvector('english', title || ' ' || body));"
    down "DROP INDEX pgweb_idx;"
  end
end

```




## postgres.custom_statements.statement
```elixir
statement name
```


Add a custom statement for migrations.




### Examples
```
statement :pgweb_idx do
  up "CREATE INDEX pgweb_idx ON pgweb USING GIN (to_tsvector('english', title || ' ' || body));"
  down "DROP INDEX pgweb_idx;"
end

```



### Arguments

| Name | Type | Default | Docs |
|------|------|---------|------|
| [`name`](#postgres-custom_statements-statement-name){: #postgres-custom_statements-statement-name .spark-required} | `atom` |  | The name of the statement, must be unique within the resource |
### Options

| Name | Type | Default | Docs |
|------|------|---------|------|
| [`up`](#postgres-custom_statements-statement-up){: #postgres-custom_statements-statement-up .spark-required} | `String.t` |  | How to create the structure of the statement |
| [`down`](#postgres-custom_statements-statement-down){: #postgres-custom_statements-statement-down .spark-required} | `String.t` |  | How to tear down the structure of the statement |
| [`code?`](#postgres-custom_statements-statement-code?){: #postgres-custom_statements-statement-code? } | `boolean` | `false` | By default, we place the strings inside of ecto migration's `execute/1` function and assume they are sql. Use this option if you want to provide custom elixir code to be placed directly in the migrations |





### Introspection

Target: `AshPostgres.Statement`


## postgres.manage_tenant
Configuration for the behavior of a resource that manages a tenant




### Examples
```
manage_tenant do
  template ["organization_", :id]
  create? true
  update? false
end

```




### Options

| Name | Type | Default | Docs |
|------|------|---------|------|
| [`template`](#postgres-manage_tenant-template){: #postgres-manage_tenant-template .spark-required} | `String.t \| atom \| list(String.t \| atom)` |  | A template that will cause the resource to create/manage the specified schema. |
| [`create?`](#postgres-manage_tenant-create?){: #postgres-manage_tenant-create? } | `boolean` | `true` | Whether or not to automatically create a tenant when a record is created |
| [`update?`](#postgres-manage_tenant-update?){: #postgres-manage_tenant-update? } | `boolean` | `true` | Whether or not to automatically update the tenant name if the record is udpated |




## postgres.references
A section for configuring the references (foreign keys) in resource migrations.

This section is only relevant if you are using the migration generator with this resource.
Otherwise, it has no effect.


### Nested DSLs
 * [reference](#postgres-references-reference)


### Examples
```
references do
  reference :post, on_delete: :delete, on_update: :update, name: "comments_to_posts_fkey"
end

```




### Options

| Name | Type | Default | Docs |
|------|------|---------|------|
| [`polymorphic_on_delete`](#postgres-references-polymorphic_on_delete){: #postgres-references-polymorphic_on_delete } | `:delete \| :nilify \| :nothing \| :restrict` |  | For polymorphic resources, configures the on_delete behavior of the automatically generated foreign keys to source tables. |
| [`polymorphic_on_update`](#postgres-references-polymorphic_on_update){: #postgres-references-polymorphic_on_update } | `:update \| :nilify \| :nothing \| :restrict` |  | For polymorphic resources, configures the on_update behavior of the automatically generated foreign keys to source tables. |



## postgres.references.reference
```elixir
reference relationship
```


Configures the reference for a relationship in resource migrations.

Keep in mind that multiple relationships can theoretically involve the same destination and foreign keys.
In those cases, you only need to configure the `reference` behavior for one of them. Any conflicts will result
in an error, across this resource and any other resources that share a table with this one. For this reason,
instead of adding a reference configuration for `:nothing`, its best to just leave the configuration out, as that
is the default behavior if *no* relationship anywhere has configured the behavior of that reference.




### Examples
```
reference :post, on_delete: :delete, on_update: :update, name: "comments_to_posts_fkey"
```



### Arguments

| Name | Type | Default | Docs |
|------|------|---------|------|
| [`relationship`](#postgres-references-reference-relationship){: #postgres-references-reference-relationship .spark-required} | `atom` |  | The relationship to be configured |
### Options

| Name | Type | Default | Docs |
|------|------|---------|------|
| [`ignore?`](#postgres-references-reference-ignore?){: #postgres-references-reference-ignore? } | `boolean` |  | If set to true, no reference is created for the given relationship. This is useful if you need to define it in some custom way |
| [`on_delete`](#postgres-references-reference-on_delete){: #postgres-references-reference-on_delete } | `:delete \| :nilify \| :nothing \| :restrict` |  | What should happen to records of this resource when the referenced record of the *destination* resource is deleted. |
| [`on_update`](#postgres-references-reference-on_update){: #postgres-references-reference-on_update } | `:update \| :nilify \| :nothing \| :restrict` |  | What should happen to records of this resource when the referenced destination_attribute of the *destination* record is update. |
| [`deferrable`](#postgres-references-reference-deferrable){: #postgres-references-reference-deferrable } | `false \| true \| :initially` | `false` | Wether or not the constraint is deferrable. This only affects the migration generator. |
| [`name`](#postgres-references-reference-name){: #postgres-references-reference-name } | `String.t` |  | The name of the foreign key to generate in the database. Defaults to <table>_<source_attribute>_fkey |
| [`match_with`](#postgres-references-reference-match_with){: #postgres-references-reference-match_with } | `keyword` |  | Defines additional keys to the foreign key in order to build a composite foreign key. The key should be the name of the source attribute (in the current resource), the value the name of the destination attribute. |
| [`match_type`](#postgres-references-reference-match_type){: #postgres-references-reference-match_type } | `:simple \| :partial \| :full` |  | select if the match is `:simple`, `:partial`, or `:full` |





### Introspection

Target: `AshPostgres.Reference`


## postgres.check_constraints
A section for configuring the check constraints for a given table.

This can be used to automatically create those check constraints, or just to provide message when they are raised


### Nested DSLs
 * [check_constraint](#postgres-check_constraints-check_constraint)


### Examples
```
check_constraints do
  check_constraint :price, "price_must_be_positive", check: "price > 0", message: "price must be positive"
end

```




## postgres.check_constraints.check_constraint
```elixir
check_constraint attribute, name
```


Add a check constraint to be validated.

If a check constraint exists on the table but not in this section, and it produces an error, a runtime error will be raised.

Provide a list of attributes instead of a single attribute to add the message to multiple attributes.

By adding the `check` option, the migration generator will include it when generating migrations.




### Examples
```
check_constraint :price, "price_must_be_positive", check: "price > 0", message: "price must be positive"

```



### Arguments

| Name | Type | Default | Docs |
|------|------|---------|------|
| [`attribute`](#postgres-check_constraints-check_constraint-attribute){: #postgres-check_constraints-check_constraint-attribute .spark-required} | `any` |  | The attribute or list of attributes to which an error will be added if the check constraint fails |
| [`name`](#postgres-check_constraints-check_constraint-name){: #postgres-check_constraints-check_constraint-name .spark-required} | `String.t` |  | The name of the constraint |
### Options

| Name | Type | Default | Docs |
|------|------|---------|------|
| [`message`](#postgres-check_constraints-check_constraint-message){: #postgres-check_constraints-check_constraint-message } | `String.t` |  | The message to be added if the check constraint fails |
| [`check`](#postgres-check_constraints-check_constraint-check){: #postgres-check_constraints-check_constraint-check } | `String.t` |  | The contents of the check. If this is set, the migration generator will include it when generating migrations |





### Introspection

Target: `AshPostgres.CheckConstraint`







<style type="text/css">.spark-required::after { content: "*"; color: red !important; }</style>
