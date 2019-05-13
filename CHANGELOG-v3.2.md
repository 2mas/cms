# Running Release Notes for Craft CMS 3.2

::: warning
This update introduces a few changes in behavior to be aware of:

- Custom login controllers must now explicitly set their `$allowAnonymous` values to include `self::ALLOW_ANONYMOUS_OFFLINE` if they wish to be available when the system is offline.
:::

### Added
- The `site` element query params now support passing multiple site handles, or `'*'`, to query elements across multiple sites at once. ([#2854](https://github.com/craftcms/cms/issues/2854))
- Added the `unique` element query param, which can be used to prevent duplicate elements when querying elements across multiple sites.
- Added `craft\web\Request::getIsLoginRequest()` and `craft\console\Request::getIsLoginRequest()`.

### Changed
- Renamed `craft\helpers\ArrayHelper::filterByValue()` to `where()`.
- Anonymous/offline/Control Panel access validation now takes place from `craft\web\Controller::beforeAction()` rather than `craft\web\Application::handleRequest()`, giving controllers a chance to do things like set CORS headers before a `ForbiddenHttpException` or `ServiceUnavailableHttpException` is thrown. ([#4008](https://github.com/craftcms/cms/issues/4008))
- Controllers can now set `$allowAnonymous` to a combination of bitwise integers `self::ALLOW_ANONYMOUS_LIVE` and `self::ALLOW_ANONYMOUS_OFFLINE`, or an array of action ID/bitwise integer pairs, to define whether their actions should be accessible anonymously even when the system is offline.

### Deprecated
- Deprecated `craft\helpers\ArrayHelper::filterByValue()`. Use `where()` instead.
- Deprecated `craft\web\Request::getIsSingleActionRequest()` and `craft\console\Request::getIsSingleActionRequest()`.
