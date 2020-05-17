# [GithubApi](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#githubapi)

----------

## [This is a work in progress!](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#this-is-a-work-in-progress)

### [_Please don't put it into production yet._](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#please-dont-put-it-into-production-yet)

----------

## [What's there?](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#whats-there)

Not a whole lot, yet. The list of examples is pretty exhaustive.

## [How do I use it?](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#how-do-i-use-it)

Start by adding it to your dependencies, then check the examples.

```toml
[dependencies]
githubapi = { git = "https://github.com/segfaultsourcery/githubapi", tag = "v0.1.0" }

```

## [Envelope](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#envelope)

### [Result type](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#result-type)

Every endpoint returns  `Result<GitHubApiResult<T>, GitHubApiError>`.

#### [GitHubApiResult](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#githubapiresult)

```rust

pub struct GitHubApiResult<T> {
    pub result: T,
    pub raw_result: String,
    pub limits: Option<LimitRemainingReset>,
    pub owner: Option<String>,
    pub repository: Option<String>,
    pub next_page: Option<u64>,
}

```

#### [GitHubApiError](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#githubapierror)

```rust

pub enum GitHubApiError {
    NotImplemented,
    JsonError(JsonError, String),
    GitHubError(String, String),
    ReqwestError(ReqwestError),
}

```

## [Examples](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#examples)

### [Get rate limit](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#get-rate-limit)

```rust

let gh = GitHubApi::new(Credentials::UsernamePassword(username, password));
let result = gh.get_rate_limit();
println!("{:#?}", result);

```

### [Get license](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#get-license)

```rust

let gh = GitHubApi::new(Credentials::UsernamePassword(username, password));
let license = gh.get_license("segfaultsourcery", "githubapi");
println!("{:#?}", license);

```

### [Get releases](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#get-releases)

```rust

let gh = GitHubApi::new(Credentials::UsernamePassword(username, password));
for page in gh.get_releases("segfaultsourcery", "githubapi") {
    println!("{:#?}", page);
}

```

### [Get tags](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/githubapi/landing.html#get-tags)

```rust

let gh = GitHubApi::new(Credentials::UsernamePassword(username, password));
for page in gh.get_tags("segfaultsourcery", "githubapi") {
    println!("{:#?}", page);
}
```