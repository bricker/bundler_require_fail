#### Description of Problem
With commit bundler/bundler@f740c40598142d990d59e129293c22c5d6f980b7 , a generic `rescue` block is wrapped around the `Kernel.require` line which loads your libraries. This block only outputs warning and debug text to `Bundler.ui`, which is [NOT VISIBLE by default](https://github.com/bundler/bundler/blob/c8c7d58a6628097bbe58dd47c11b5e9dc25c897a/lib/bundler.rb#L95-L97).

So, if the file being required throws any error inheriting from `StandardError` (most errors), the error is by default silently ignored and the file isn't loaded. This gives you confusing, unrelated errors that tell you nothing about the actual problem.

#### Reproduce
1. Clone repo
2. Run `bundle install`
3. Run `bundle exec rspec`

#### Expected Result
Runtime failure with `NameError: uninitialized constant BundlerRequireFail_WHOOPS_TYPO`

#### Actual Result
The test will fail with `uninitialized constant AnotherModule`

To see the test pass, fix the module name in `bundler_require_fail/failure.rb` from `BundlerRequireFail_WHOOPS_TYPO` to `BundlerRequireFail`. Run the test again and it will pass.
