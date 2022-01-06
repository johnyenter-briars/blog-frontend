---
title: First Blog Post
date: 2021-12-05
---

### My First Post

As a first post, I thought it would be fun to be a little meta, and cover the pipeline/tech stack of my blog itself.

For my blog, I needed 5 major features:

1. The ability to apply beautiful themes quickly and cleanly
2. Easy to make posts (preferably in markdown)
2. Remote hosting with low compute times
3. Serving of the blog via a web application, as opposed to static files
4. Networking saftey and best practices

If I could make it work, I **wanted** 2 more features:

1. The ability to interop with [Reverse Date Parser](/rdp), the application I am building
2. [Rust](https://www.rust-lang.org/) to be involved somehow

In order to meet these features, I decided on the following tech stack:

| Feature | Solution |
| --- | ----------- |
| Themes/Markdown | [Hexo](https://hexo.io/) |
| Remote Hosting | [Digital Ocean](https://www.digitalocean.com/) |
| Dynamic Serving | [Rocket](https://rocket.rs/) |

#### Complete Picture

I use Hexo to write posts in markdown and develop the themeing. This then gets compiled to a static html/css files which gets copied over to a folder within a Rocket project. (If you've never heard of Rocket before, its a web application framework built in Rust). 

I then spin up a rocket server to serve the static files over localhost. To make sure that the application remains secure, it runs over a service account without root privledges. An Nginx server sits in front of the rocket application, forwarding http requests from port 80 to port 8000. This is because on a linux system, the application needs root privledges to run on ports 80 and 443 (and others I think).

Reverse date parser follows a similar format, as its a [React](https://reactjs.org/) app that gets compiled to static files, and served via the Rocket server.

This package is uploaded and hosted through an Ubuntu server living on Digital Ocean, with my domain name pointing to the server's IP via an A DNS record. 

#### Submodules

You'll notice that we've got multiple different applications that are conceptually separate, but nevertheless need to get packaged together in a final build. The natural (I think?) solution for this was to use [Git Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

Before building this blog, I had 0 experience with submodules, and even now I still can't say I fully understand them. But the basic idea is that a git repo can have a reference to a certian commit of a different repo. This allows dependent repos to be tracked in isolated source control.


#### Putting it all Together

Words aren't fun to look at, so I made a diagram (to the best of my artistic ability) of the process:

![](/images/diagram1.png)

#### Fun Sidenotes

Since the blog is served at `/` and Reverse Date Parser is served at `/rdp`, this causes a ranking conflict. Since any path for `/rdp` includes `/`. In order to solve this, I had to give each path rankings in Rocket.

```rust
fn rocket() -> _ {
    rocket::build()
        .mount("/", FileServer::from(relative!("public")).rank(1))
        .mount("/rdp", FileServer::from(relative!("rdp")).rank(2))
}
```




