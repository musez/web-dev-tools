# DOM操作

1. 是否有class
    ```javascript
    /**
     * @desc 是否有class
     * @param {Object} obj
     * @param {String} cls
     * @returns {Boolean}
     */
    function hasClass(obj, cls) {
        cls = cls.replace(/^\s|\s$/g, "")
        return (" " + ((obj || {}).className || "").replace(/\s/g, " ") + " ").indexOf(" " + cls + " ") >= 0;
    }
    ```

2. 添加class
    ```javascript
    /**
     * @desc 添加class
     * @param {Object} obj
     * @param {String} cls
     */
    function addClass(obj, cls) {
        if (!this.hasClass(obj, cls)) obj.className += " " + cls;
    }
    ```

3. 删除class
    ```javascript
    /**
     * @desc 删除class
     * @param {Object} obj
     * @param {String} cls
     */
    function removeClass(obj, cls) {
        cls = cls.replace(/^\s|\s$/g, "");
    
        if ((" " + ((obj || {}).className || "").replace(/\s/g, " ") + " ").indexOf(" " + cls + " ") >= 0) {
            var reg = new RegExp('(\\s|^)' + cls + '(\\s|$)');
            obj.className = obj.className.replace(reg, ' ');
        }
    }
    ```
    
4. 获取指定元素的子元素
    ```javascript
    /**
     * 获取指定元素的子元素
     * @param {object} curEle
     * @param {string} tagName
     * @returns {Array}
     */
    function children (curEle, tagName) {
        var nodeList = curEle.childNodes;
        var ary = [];
        if (/MSIE(6|7|8)/.test(navigator.userAgent)) {
            for (var i = 0; i < nodeList.length; i++) {
                var curNode = nodeList[i];
                if (curNode.nodeType === 1) {
                    ary[ary.length] = curNode;
                }
            }
        } else {
            ary = Array.prototype.slice.call(curEle.children);
        }
    
        // 获取指定子元素
        if (typeof tagName === "string") {
            for (var k = 0; k < ary.length; k++) {
                var curTag = ary[k];
                if (curTag.nodeName.toLowerCase() !== tagName.toLowerCase()) {
                    ary.splice(k, 1);
                    k--;
                }
            }
        }
    
        return ary;
    }
    ```

5. 父子iframe通信
    ```javascript
    // 调用父iframe的方法
    parent.frames['searchListIframe'].methodName();
    
    // 获取父iframe的dom
    $(parent.frames["filterFrame"].document).contents()).find("selectorName");
    ```
