<script lang="ts">
import { open as DialogOpen } from '@tauri-apps/api/dialog';
import { readBinaryFile, writeBinaryFile } from '@tauri-apps/api/fs';
// import { randomBytes, createCipheriv, createDecipheriv } from "crypto";
// import { Buffer } from "buffer"
import { AES, Random } from "@nfen/webcrypto-ts";

export default {
    data: function () {
        return {
            filePath: "",
            password: "",
            option: "decrypt",
        }
    },
    methods: {
        getFile: async function () {
            console.log("choosing file");
            const file = await DialogOpen({
                multiple: false,
            });
            this.filePath = <string>file;
        },
        // generateKey: async function () {
        //     const key = await AES.AES_CBC.generateKey();
        //     const exp = <ArrayBuffer>await AES.AES_CBC.exportKey("raw", key);
        //     console.log(exp);
        //     const dec = new TextDecoder("utf-8");
        //     this.password = dec.decode(exp);

        //     // this.password = (await AES.AES_CBC.exportKey("raw", key)).toString();
        // },
        startOperation: async function () {
            console.log(this.password);
            console.log(this.option);
            if (this.password == "") {
                alert("Password is empty");
                return;
            }
            if (this.filePath == "") {
                alert("File is empty");
                return;
            }
            // if (this.option == "encrypt") {
            //     console.log("encrypting");
            //     const file = await readBinaryFile(this.filePath);
            //     // encrypt file with aes 256 cbc
            //     const iv = await Random.IV.generate(16);
            //     const enc = new TextEncoder();
            //     const psw = enc.encode(this.password);
            //     const key = await AES.AES_CBC.importKey("raw", psw, { length: 256 });
            //     const ciphertextBytes = await AES.AES_CBC.encrypt({ iv }, key, file);
            //     const path = this.filePath.split(".");
            //     const newPath = `${path[0]}_enc.${path[1]}`;
            //     writeBinaryFile(newPath, ciphertextBytes);
            // }
            else if (this.option == "decrypt") {
                try {

                    console.log("decrypting");
                    const file = await readBinaryFile(this.filePath);
                    const keyArray = new Uint8Array(this.password.match(/[\da-f]{2}/gi)!.map((h) => parseInt(h, 16)));
                    const iv = file.slice(0, 16);
                    const encrypted = file.slice(16);
                    const key = await AES.AES_CBC.importKey("raw", keyArray, { length: 256 });
                    console.log("key", key);
                    const decrypted = await AES.AES_CBC.decrypt({ iv }, key, encrypted);
                    console.log("decrypted", decrypted);
                    const path = this.filePath.split(".");
                    const newPath = `${path[0]}_dec.${path[1]}`;
                    await writeBinaryFile(newPath, decrypted);
                } catch (error) {
                    console.log(error);
                }
                //     console.log(file)
                //     // decrypt file with aes 256 cbc
                //     const iv = file.slice(0, 16);
                //     const encrypted = file.slice(16);
                //     var typedArray = new Uint8Array(this.password.match(/../g)?.map(h=>parseInt(h,16))??[]).buffer
                //     const enc = new TextEncoder();
                //     const psw = enc.encode(this.password);
                //     console.log(typedArray);
                //     const key = await AES.AES_CBC.importKey("raw", typedArray, { length: 256 });
                //     const decrypted = await AES.AES_CBC.decrypt({ iv }, key, encrypted);
                //     // write decrypted file
                //     const path = this.filePath.split(".");
                //     const newPath = `${path[0]}_dec.${path[1]}`;
                //     writeBinaryFile(newPath, decrypted);
            }
        }

    }
}
</script>

<template>
    <!-- <div class="row"> -->
    <button type="button" v-on:click="getFile">Select a file</button>
    <br />
    <input type="text" id="password" v-model="password" />
    <!-- <button type="button" v-on:click="generateKey">Generate key</button> -->
    <br />
    <!-- OPTION LIST ENCRYPT AND DECRYPT -->
    <select id="option" v-model="option">
        <!-- <option value="encrypt">Encrypt</option> -->
        <option value="decrypt">Decrypt</option>
    </select>
    <br />
    <button id="button" v-on:click="startOperation">Start</button>
    <!-- </div> -->
</template>