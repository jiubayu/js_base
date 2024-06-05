<template>
  <div>复制内容:{{ copyContent }} 黏贴内容:{{ pasteContent }}</div>
  <div>
    <textarea></textarea>
  </div>

  黏贴图片
  <img ref="img" :src="pasteImage"/>
</template>

<script>
export default {
    name: 'Keyboard',
    data(){
        return {
            copyContent: '',
            pasteContent: '',
            pasteImage: '',
        }
    },
    mounted() {
        document.body.oncopy = (event) => {
            const selection = document.getSelection();
            event.clipboardData.setData(
                'text/plain',
                '该文档不允许复制剪贴操作，谢谢配合！' + selection.toString(),
            )
        }
        document.body.onpaste = (event) => {
            this.pasteContent = event.clipboardData.getData('text/plain');
            if(event.clipboardData.items) {
                [...event.clipboardData.items].forEach((item) => {
                    if(item.type.includes('image')) {
                        let file = item.getAsFile(); 
                        console.log(file, 'file---')

                        var reader = new FileReader();
                        reader.onload = (e) => {
                            this.$refs.img.style.width = file.width + 'px';
                            this.$refs.img.style.height = file.height + 'px';
                            this.pasteImage = e.target.result;
                            console.log(e.target, 'target--')
                        };
                        reader.onerror = (err) => {
                            console.log(err);
                        }
                        reader.readAsDataURL(file);
                    }
                })
            }
        }
    }
};
</script>

<style lang="scss" scoped></style>
