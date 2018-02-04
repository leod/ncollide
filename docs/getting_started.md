# Getting started
**ncollide** relies on the official Rust package manager
[Cargo](http://crates.io) for dependency resolution and compilation. Therefore,
making **ncollide** ready to be used by your project is simply a matter of
adding a new dependency to your `Cargo.toml` file. Note that you will probably
need **nalgebra** version 0.13.0 as well because it defines algebraic entities
(vectors, points, transformation matrices) used by most types of **ncollide**.

```toml
[dependencies]
nalgebra = "0.14.0"
ncollide = "0.14.0"
```

Until **ncollide** reaches 1.0, it is strongly recommended to always use its
latest version, though you might encounter breaking changes from time to time.
Once your `Cargo.toml` file is set up, the corresponding crate must be imported
by your project with the usual `extern crate` directive:
```rust
extern crate ncollide;
```

## Cargo example
You may use this `Cargo.toml` file to compile the downloadable examples of this
guide. Simply replace `example.rs` by the actual example's file name.

<ul class="nav nav-tabs">
  <li class="active"><a id="tab_nav_link" data-toggle="tab" href="#cargo">Example</a></li>

  <div class="btn-primary" onclick="window.open('https://raw.githubusercontent.com/sebcrozet/ncollide/gh-pages/src/cargo/Cargo.toml')"></div>
</ul>

<div class="tab-content" markdown="1">
  <div id="cargo" class="tab-pane in active">
```toml
[package]
name    = "example-using-ncollide"
version = "0.0.0"
authors = [ "You" ]

[dependencies]
approx   = "0.1.0"
alga     = "0.5.0"
nalgebra = "0.14.0"
ncollide = "0.14.0"

[[bin]]
name = "example"
path = "./example.rs"
```
  </div>
</div>

# Project structure
The **ncollide** crate is only an interface for several, smaller crates part of
the **ncollide** project. Thus if only a subset of the features is of interest
to you, you may directly depend any of them individually:

Crate name                  | Description
----------------------------|-------------
**ncollide_math**           | Traits that must be satisfied by algebraic entities used by the whole project. |
**ncollide_utils**          | [Miscellaneous](../miscellaneous) data structures and basic geometrical operations needed by all the other crates. |
**ncollide_geometry**       | The geometric kernel of **ncollide**. It defines [shapes](../geometric_representations), [bounding volumes](../bounding_volumes), structures for [spacial partitioning](../bounding_volumes/#spacial-partitioning), and [geometric queries](../geometric_queries) operating on all of them. |
**ncollide_procedural**     | Procedural [mesh generation](mesh_generation/#mesh-generation) from parameters provided by the user. |
**ncollide_transformation** | Operators that create an alternative geometrical representation of a shape or mesh given in input. This includes [convex hull](../mesh_generation/#convex-hull), [convex decomposition](../mesh_generation/#convex-decomposition), and shapes discretization. |
**ncollide_pipeline**       | Persistent structures for recurrent geometric queries. This exploits time coherence and implements explicitly the concepts of [broad phase](collision_detection_pipeline/#broad-phase) and [narrow phase](collision_detection_pipeline/#narrow-phase). This also includes the [collision world](collision_detection_pipeline/#collision-world) which is the main interface between the user **ncollide**. |

To use any of those crates, simply add a corresponding dependency entry to your
`Cargo.toml`. Note that you should not expect the version numbers of those
crates to be identical. For example, **ncollide** being in version `0.14.0` does
not imply that **ncollide_geometry** (say) is at its version `0.14.0` as well.
