# Google AngularJS 代码规范

> 官方文档：https://google.github.io/styleguide/angularjs-google-style.html

---

## 目录

- [命名规范](#命名规范)
- [模块组织](#模块组织)
- [控制器](#控制器)
- [服务](#服务)
- [指令](#指令)

---

## 命名规范

### 文件命名

- 使用 **kebab-case**
- 文件类型作为后缀

```
// 正确
user-profile.component.js
user-service.service.js
user-list.directive.js
```

### 组件命名

- 使用 **PascalCase**

```javascript
// 正确
class UserProfileComponent {}
```

### 服务命名

- 使用 **PascalCase**

```javascript
// 正确
class UserService {}
class HttpInterceptor {}
```

---

## 模块组织

### 模块定义

```javascript
// 正确
angular.module('myApp', [
    'ngRoute',
    'ngAnimate',
    'myApp.services',
    'myApp.directives'
]);
```

### 模块结构

```
my-app/
├── app.module.js
├── app.config.js
├── components/
│   ├── user-profile/
│   │   ├── user-profile.component.js
│   │   └── user-profile.template.html
│   └── user-list/
├── services/
│   ├── user.service.js
│   └── http.service.js
└── directives/
    └── my-directive.directive.js
```

---

## 控制器

### 使用 controllerAs

```javascript
// 正确
angular.module('myApp')
    .controller('UserProfileController', UserProfileController);

function UserProfileController() {
    var vm = this;
    vm.userName = 'John';
    vm.save = save;

    function save() {
        // ...
    }
}
```

### 避免 $scope

```javascript
// 错误
angular.module('myApp')
    .controller('MyController', function($scope) {
        $scope.userName = 'John';
    });

// 正确
angular.module('myApp')
    .controller('MyController', function() {
        var vm = this;
        vm.userName = 'John';
    });
```

---

## 服务

### 使用 factory 或 service

```javascript
// 正确 - factory
angular.module('myApp')
    .factory('UserService', UserService);

function UserService($http) {
    return {
        getUser: getUser,
        saveUser: saveUser
    };

    function getUser(id) {
        return $http.get('/api/users/' + id);
    }

    function saveUser(user) {
        return $http.post('/api/users', user);
    }
}
```

---

## 指令

### 命名和定义

```javascript
// 正确
angular.module('myApp')
    .directive('myDirective', myDirective);

function myDirective() {
    return {
        restrict: 'E',
        templateUrl: 'my-directive.template.html',
        scope: {
            data: '='
        },
        controllerAs: 'vm',
        bindToController: true,
        controller: MyDirectiveController
    };
}

function MyDirectiveController() {
    var vm = this;
    // ...
}
```

---

## 参考资料

- [Google AngularJS Style Guide (官方)](https://google.github.io/styleguide/angularjs-google-style.html)

---

*本文档基于 Google AngularJS Style Guide 整理*
