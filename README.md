Inject dependencies into ZF2 services via configuration rather than factory classes.
======

Example of constructor injection with the service name being the same as its class name:
```php
'service_manager' => [

    'config_factories' => [
    
        'App\Email\EmailService' => [
            'arguments' => [
                'Name\Of\A\Service\I\Want\To\Inject',
                'Name\Of\A\AnotherService\I\Want\To\Inject'
            ],
        ]
        
    ]
    
    'invokables' => [
        //... Other ZF2 services here
    ],

    'factories' => [
        //... Other ZF2 services here
    ]
]
```

Example usage with all options:
```php
// in module.config.php
'controllers' => [

    // This is a special config key that RmFactoriesAsConfiguration reads.
    'config_factories' => [
    
        // This is the name of the service.
        'EmailTemplateApiController' => [
        
            /**
             * This is the service's  class name.
             * Not required if the service's name is the same as its class name.
             */
            'class' => 'App\Controller\EmailTemplateApiController',
            
            /**
             * This is an array of service names that the class's constructor takes.
             * Not required if the service's constructor takes no arguments.
             */
            'arguments' => ['Name\Of\A\Service\I\Want\To\Inject'],
            
            /** 
             * This is an array of setters to call mapped to service names to inject into each setter.
             * Not required if your service has no setters.
             */ 
            'calls' => [
                'setFunService' => ['Name\Of\Another\Service\I\Want\To\Inject']
            ]
        ]
    ],
]
```
