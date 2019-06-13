optimization: {
    splitChunks: { 
      chunks: "initial",         // 代码块类型 必须三选一： "initial"（初始化） | "all"(默认就是all) | "async"（动态加载） 
      minSize: 0,                // 最小尺寸，默认0
      minChunks: 1,              // 最小 chunk ，默认1
      maxAsyncRequests: 1,       // 最大异步请求数， 默认1
      maxInitialRequests: 1,     // 最大初始化请求书，默认1
      name: () => {},            // 名称，此选项课接收 function
      cacheGroups: {                // 缓存组会继承splitChunks的配置，但是test、priorty和reuseExistingChunk只能用于配置缓存组。
        priority: "0",              // 缓存组优先级,即权重 false | object |
        vendor: {                   // key 为entry中定义的 入口名称
          chunks: "initial",        // 必须三选一： "initial"(初始化) | "all" | "async"(默认就是异步)
          test: /react|lodash/,     // 正则规则验证，如果符合就提取 chunk
          name: "vendor",           // 要缓存的 分隔出来的 chunk 名称
          minSize: 0,
          minChunks: 1,
          enforce: true,
          reuseExistingChunk: true   // 可设置是否重用已用chunk 不再创建新的chunk
        }
      }
    }
  }

 splitChunks: {
      chunks: 'all',   // initial、async和all
      minSize: 30000,   // 形成一个新代码块最小的体积
      maxAsyncRequests: 5,   // 按需加载时候最大的并行请求数
      maxInitialRequests: 3,   // 最大初始化请求数
      automaticNameDelimiter: '~',   // 打包分割符
      name: true,
      cacheGroups: {
        vendor: {
          name: "vendor",
          test: /[\\/]node_modules[\\/]/, //打包第三方库
          chunks: "all",
          priority: 10 // 优先级
        },
        common: { // 打包其余的的公共代码
          minChunks: 2, // 引入两次及以上被打包
          name: 'common', // 分离包的名字
          chunks: 'all',
          priority: 5
        },
      }
    },


  cacheGroups: {
        reactBase: {
          name: 'reactBase',
          test: (module) => {
              return /react|redux/.test(module.context);
          },
          chunks: 'initial',
          priority: 10,
        },
        utilBase: {
          name: 'utilBase',
          test: (module) => {
              return /rxjs|lodash/.test(module.context);
          },
          chunks: 'initial',
          priority: 9,
        },
        uiBase: {
          name: 'chartBase',
          test: (module) => {
              return /echarts/.test(module.context);
          },
          chunks: 'initial',
          priority: 8,
        },
        commons: {
          name: 'common',
          chunks: 'initial',
          priority: 2,
          minChunks: 2,
        },
      }

作者：寻找海蓝96
链接：https://juejin.im/post/5d00820b5188255ee806a1c7
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

HashedModuleIdsPlugin
<script src="https://cdn.polyfill.io/v2/polyfill.min.js"></script> //动态