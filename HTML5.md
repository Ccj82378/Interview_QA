# HTML5

## 1. Attribute vs Property
- Attribute(特性)由HTML定義，所有出現在HTML標籤內的描述節點都是attribute
    ```
    <div id="test" class="button" custom-attr="1"></div>
    ```
    以上有三個attribute
- Property(屬性)為DOM物件自定義新增的屬性，property可以是任意型別，最後返回的都是字元型別
    ```
    HTMLInputElement.id === 'the-input'
    HTMLInputElement.type === 'text'
    HTMLInputElement.value === 'Name:'
    ```
- Attribute會始終保持html代碼中的初始值，而Property是有可能變化的
    ```
    // attribute still remains the original value
    input.getAttribute('id') // the-input
    input.getAttribute('type') // typo
    input.getAttribute('value') // Name:

    // property is a different story
    input.id // the-input
    input.type //  text
    input.value // Jack
    ```
