# Magento Helpers v2

## Service Helpers.
This service is used to help some activities during your work, which contains several functions that may make your job simpler.
Personally, this library is used for magento.

## Require
This library requiring **[Laminas Log](https://github.com/laminas/laminas-log)** for create logger.
## Installation

#### - Set Config to composer.json (not a mandatory)
```bash
composer config repositories.sirclo-bachtiar/magento-helpers-v2 git git@github.com:sirclo-bachtiar/magento-helpers-v2.git
```

#### - Install library
```bash
composer require sirclo-bachtiar/magento-helpers-v2
```

## Usage
- ### Logger Service

- #### LogService::class
It's used for create log activity.
```bash
use Bachtiar\Helper\LaminasLogger\Service\LogService;

class LogServiceTest
{
    public function Log()
    {
        return LogService::channel('default')
            ->mode('default')
            ->title('log_title')
            ->log('message_to_log');
    }
}

#### Info ####
:: channel('default') => not required
    -> select channel, available [ emerg, alert, crit, err, warn, notice, info ], if null then auto set to default.

:: mode('default') => not required
    -> select log mode, available [ test, debug, develop ], if null then auto set to default.

:: title('default') => not required
    -> set log title, if null then auto set to default title.

:: log('default') => required
    -> set log message, if null then auto set to default message.

```

- #### SwiftLog::trait
It's use for logging activity based on Icube Custom Swift Log Rule.
``` bash
use Bachtiar\Helper\LaminasLogger\Service\SwiftLog;

class SwiftLogTest
{
    use SwiftLog;

    public function __invoke()
    {
        return $this->channel('default')
            ->mode('default')
            ->classLimit('default')
            ->group('group_title')
            ->title('log_title')
            ->log('message_to_log');
    }
}

#### Info ####
:: channel('default') => not required
    -> select channel, available [ emerg, alert, crit, err, warn, notice, info ], if null then auto set to default.

:: mode('default') => not required
    -> select log mode, available [ test, debug, develop ], if null then auto set to default.

:: classLimit('default') => not required
    -> set module class namespace limit, if null then auto set to default.

:: group('default') => not required
    -> set group of log, if null then auto set to default.

:: title('default') => not required
    -> set log title, if null then auto set to default title.

:: log('default') => required
    -> set log message, if null then auto set to default message.
```

- ### Query Builder Service
It's used for custom query builder. (return query only).
```bash
use Bachtiar\Helper\CustomQueryGenerator\Service\QueryBuilderService;

class QueryBuilderTest
{
    public function __invoke()
    {
        return QueryBuilderService::select()
            ->from('base_table')
            ->join('relation_table', 'base_table.baseColumnId', '=', 'relation_table.relationColumnId')
            ->where('base_table.name', '=', 'test')
            ->andWhere('base_table.age', '=', 'age')
            ->orWhere('relation_table.address', 'like', '%ponorogo%')
            ->generate();
    }
}

#### Info ####
:: select() -> optional
    -> set select column, if null, then auto set to all (*).

:: from('base_table') -> ! must be included
    -> set base table query.

:: join('relation_table', 'baseColumnId', '=', 'relationColumnId')
    -> set inner join from query.

:: where('base_table.name', '=', 'test') -> optional
    -> set where clause from query

:: andWhere('base_table.age', '=', 'age') -> optional
    -> set or where clause from query

:: orWhere('relation_table.address', 'like', '%ponorogo%') -> optional
    -> set and where clause from query

:: generate()
    -> process to create query builder.
```
