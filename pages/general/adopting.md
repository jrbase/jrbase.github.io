# Adopting AIPs in your company

**Note:** We're working on some tooling to make this better. Keep an eye on
[this GitHub issue][] for progress.

While AIPs originated at Google and were aimed for Googlers writing Google
APIs, much of the guidance documented is useful outside of Google. This
document describes how you might adopt AIPs as the way you document your own
APIs even if you don't work at Google.
虽然 AIP 起源于 Google，并针对编写 Google API 的 Google 员工，但文档中的大部分指南在 Google 之外都是有用的。 本文档描述了即使您不在 Google 工作，您也可以如何采用 AIP 作为您记录自己的 API 的方式。

## The problem

Sometimes private organizations might have API guidance that they don't want or
care to share with the rest of the world. For example, maybe in your company
(let's say, Acme, Inc), you identify your resources with a special field called
`string acme_id`.
y有时，私有的组织也许会使用这个API但是他们不想要分享给世界上的其他人。例如，也许你的公司(比如叫做Acme, Inc)，你用一个叫做的特殊字段来识别你的资源
`string acme_id`。

This rule could be written as an AIP, but there's no reason to share this rule
with everyone -- it's only for you and your development team. However, you
don't want this to conflict with a future AIP (e.g., if you make this AIP-1234,
maybe that AIP will get written in the future and then you'll have a conflict).
So what do you do?
这条规则可以写成 AIP，但没有理由与所有人分享这条规则——它只适用于您和您的开发团队。 但是，您不希望这与未来的 AIP 发生冲突（例如，如果您制作了此 AIP-1234，那么该 AIP 可能会在将来被编写，然后您就会发生冲突）。 所以你会怎么做？

## The 9000 block

Much like the Unicode specification, we've reserved the 9000 block of AIP
numbers (that is, AIP-9000 through AIP-9999) to be for "internal use". This
means that these AIPs will never have public documentation and are free for
private companies to use for their own API guidance. As a result, all you have
to do is write your AIPs as usual and give them a number in the 9000 block.
很像 Unicode 规范，我们保留了 AIP 的 9000 块编号（即 AIP-9000 到 AIP-9999）供“内部使用”。
这意味着这些 AIP 将永远不会有公共文档，并且私人公司可以免费使用它们自己的 API 指南。


## Custom AIP domains

We're working on a separate fork-able repository that you can copy and use as
your 9000 block AIP repository. The page rendered by GitHub Pages will serve
only the AIPs in that block and redirect all other pages to [aip.dev][].
我们正在开发一个单独的可分叉存储库，您可以将其复制并用作您的 9000 块 AIP 存储库。 GitHub Pages 呈现的页面将仅提供该块中的 AIP，并将所有其他页面重定向到 [aip.dev][]。

In short, this means that you can create your own AIP domain (e.g.,
`aip.example.com`) and point that to the forked GitHub repository which will
redirect for all well-known AIPs and serve all internal AIPs from your own
repository. Once you've done that, you can cite all AIPs specifically using
that domain name (e.g., `aip.example.com/1234`) and you'll always get sent to
the right place.
简而言之，这意味着您可以创建自己的 AIP 域（例如，`aip.example.com`）并将其指向分叉的 GitHub 存储库，该存储库将为所有知名 AIP 重定向并从您自己的存储库提供所有内部 AIP . 完成此操作后，您可以引用所有专门使用该域名的 AIP（例如，`aip.example.com/1234`），您将始终被发送到正确的位置。

## Forking AIP

You can fork the AIP project and run it in your own domain if necessary. This
will allow you to customize the AIPs to your organization's needs. Or you could
use the infrastructure to create your own set of AIPs.

### Updating the URL

To run the AIP infrastructure as a GitHub Page in a another repository, the
`_config.yaml` file must be updated to work correctly in the new repo.

If a new custom domain and CNAME have been created for your AIP, only the `url`
property will need to be updated to the new domain.

```
url: https://aip.dev
```

If you are not creating a new domain, it will be necessary to add the `baseurl`
property to the `_config.yaml`. This property should contain any additional
path information that may be appended to the domain in the `url`.

For example, assume GitHub user jdoe123 forked the aip project into a
repository named my-aips. If this user served the content from their master
branch, the url to the GitHub pages would be
`https://jdoe123.github.io/my-aips/`. The accompanying `_config.yaml` would be
configured as follows:

```
url: https://jdoe123.github.io
baseurl: /my-aips
```

For more information about about how these values are used by GitHub Pages, see
the [release notes][] that standardized these configurations in Jekyll.

### Configuring Navigation

The navigation headers and bar are generated dynamically based on the
`_data/header.yaml` and `_data/nav.yaml` files respectively.

The schema for the navigation bar can be viewed under
`assets/schemas/nav-schema.yaml`. It supports two types of navigation
components; `static_group` and `matter_group`. A `static_group` menu component
will always show the same navigation elements, regardless of the content of the
page and the repository. A `matter_group` component is generated dynamically
based on the AIPs in the domain, or the current page in the site. The
configurations for a `matter_group` can be viewed in the
`assets/schemas/nav-components.yaml#defintions/matter_group` schema.

The header is just a specially rendered `static_group` component. The schema
can be viewed at `assets/schemas/static_group.yaml`.

### Testing Configuration

The `tests` folder contains an npm test module that will validate your data
files. Running these tests requires npm and mocha. Once these are installed
that tests can be ran with the `npm test` command.

<!-- prettier-ignore-start -->
[this github issue]: https://github.com/googleapis/aip/issues/98
[npm]: https://www.npmjs.com/get-npm
[mocha]: https://www.npmjs.com/package/mocha
[release notes]: https://jekyllrb.com/news/2016/10/06/jekyll-3-3-is-here/#2-relative_url-and-absolute_url-filters
<!-- prettier-ignore-end -->
