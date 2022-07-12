# Steroids for ydb client

## Migration

```rust 
let mut migrator = Migrator::new_from_dir(&include_dir!("$CARGO_MANIFEST_DIR/test-migration"));
migrator.migrate(&mut client).await.unwrap();
```

## Query macros

```rust
query!("insert into a (id) values($id)", id=>id)
```

## Select macros

```rust 
let result: Vec<i32> = select!(client.table_client(), query!("select id from a"), id=>i32)
.await
.unwrap();
```

## Update macros

```rust 
update!(
client.table_client(),
    query!("insert into a (id) values($id)", id=>id)
)
```

## Test container

Enable feature test_container

```rust
let (_node, client) = get_or_create_ydb_instance("should_create_docker_and_connect").await;

```