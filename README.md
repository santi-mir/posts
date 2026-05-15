# Posts

Short posts on topics related to AI, XAI, and AI for chemistry.

**URL**: <https://santi-mir.github.io/posts>.

## Details

-  **Build**: it builds on `./docs`. The packages needed for building from the source markdown files are:
   ```bash
   cargo install mdbook mdbook-mermaid mdbook-katex
   ```

- **License**: All the content here is under [CC BY 4.0], except for quotations which may share the license of the source.
- **Contributions**: Contributions are taken under the same license, [CC BY 4.0].
- **Tools**: [`mdbook.rs`][mdbook] builds the book and [`mdbook-mermaid.rs`][mermaid] a plugin to insert graphs.

## Development

<details>
  <summary>
    Steps
  </summary>
  
  Besides the build-apps, install:

```text
cargo install lychee rumdl caesiumclt
```

It's useful to have a pre-commit git hook

```bash
#!/bin/env bash
rumdl check
mdbook build
```

And pre-push

```bash
#!/bin/env bash
lychee src || exit 1
caesiumclt --lossless -O bigger src/assets/*.{jpg,jpeg,png} --same-folder-as-input
```

Then do `chmod +x .git/hooks/{pre-push,pre-commit}`

</details>

[mdbook]: https://github.com/rust-lang/mdBook
[mermaid]: https://github.com/orgs/mermaid-js
[CC BY 4.0]: https://creativecommons.org/licenses/by/4.0/
