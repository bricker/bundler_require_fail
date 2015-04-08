#### Reproduce
1. Clone repo
2. Run `bundle install`
3. Run `bundle exec rspec`

#### Expected Result
Runtime failure with `NameError: uninitialized constant BundlerRequireFail_WHOOPS_TYPO`

#### Actual Result
The test will fail with `uninitialized constant AnotherModule`

To see the test pass, fix the module name in `bundler_require_fail/failure.rb` from `BundlerRequireFail_WHOOPS_TYPO` to `BundlerRequireFail`. Run the test again and it will pass.
