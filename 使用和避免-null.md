# 使用和避免 null

轻率地使用 `null ` 可能会导致很多令人惊愕的bugs。通过学习 Google 底层代码库，我们发现 95%的集合类不接
受 `null ` 值作为元素。我们认为， 相比默默地接受 `null ` ，使用快速失败操作拒绝 `null ` 值对开发者更有帮助。

此外，`null ` 的含糊语义让人很不舒服。`null ` 很少可以明确地表示某种语义，例如，`Map.get(key)`返回 `null `
时，可能表示 map 中的值是 `null ` ，亦或 map 中没有 key 对应的值。`null ` 可以表示失败、成功或几乎任何情
况。使用 `null ` 以外的特定值，会让你的逻辑描述变得更清晰。

`null ` 确实也有合适和正确的使用场景，如在性能和速度方面 `null ` 是廉价的，而且在对象数组中，出现 `null ` 也是
无法避免的。但相对于底层库来说，在应用级别的代码中，`null ` 往往是导致混乱，疑难问题和模糊语义的元
凶，就如同我们举过的 `Map.get(key)`的例子。最关键的是，`null ` 本身没有定义它表达的意思。

鉴于这些原因，很多 Guava 工具类对 `null ` 值都采用快速失败操作，除非工具类本身提供了针对 `null ` 值的因变措

施。此外，Guava 还提供了很多工具类，让你更方便地用特定值替换 `null ` 值。