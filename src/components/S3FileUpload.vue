<template>
    <div>
        <h3>Subida de elementos</h3>
        <div v-if="file_video">
            <video
            class="container-video"
            controls
            :src="file_video"
            />
        </div>
        <input type="file" @change="upload_file(fieldName,$event.target.files)">
    </div>
</template>

<script>
import S3 from 'aws-s3';

export default {
    data() {
        return {
            file_video: null,
        }
    },  
    computed: {
        config() {
            return {
                bucketName: 'bucketinnovatest',
                region: 'us-east-1',
                dirName: this.dirName,
                accessKeyId: 'AKIAXZD67YO6HXG2SG6T',
                secretAccessKey: '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',
                s3Url: 'https://bucketinnovatest.s3.amazonaws.com', /* optional */
            }
        },
        baseURL() {
            return 'https://innovabucket11.s3.amazonaws.com';
        },
        S3Client() {
            return new S3(this.config);
        },
        newFileName() {
            return Math.random().toString().slice(2)
        },
        url() {
            return `${this.baseURL}/${this.dirName}`;
        }
    },
    methods: {
        upload_file(fieldName,files) {
            let file = files[0];
            console.log(file);

            let nameExtension = file.name.split('.')[0];
            let fileExtension = file.type.split('/')[1];
            this.S3Client
                .uploadFile(file,nameExtension).finally(() => {
                    this.obj[fieldName] = `${this.url}/${nameExtension}.${fileExtension}`;
                })
        }
    },
    props: ['obj','dirName']
}
</script>

<style lang="scss">
</style>