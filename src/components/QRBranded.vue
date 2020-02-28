<template>
  <div ref="qr"></div>
</template>

<script>
import QRCode from "@keeex/qrcodejs-kx";

export default {
  props: {
    brandImageSrc: String,
    text: String,
    size: {
      type: Number,
      default: 300
    },
    colorDark: {
      type: String,
      default: "#000"
    },
    colorLight: {
      type: String,
      default: "#fff"
    },
    errorLevel: {
      type: String,
      validator: function(value) {
        return value === "L" || value === "M" || value === "Q" || value === "H";
      },
      required: false,
      default: "H"
    }
  },
  data() {
    return {
      image: ""
    };
  },
  mounted() {
    this.drawBrandedQRCode();
  },
  methods: {
    drawBrandedQRCode() {
      const brandImage = new Image();

      const qrCodeWrapper = document.createElement("div");
      this.renderQRCodeinto(qrCodeWrapper);

      qrCodeWrapper.children[1].addEventListener("load", () => {
        const qrCodeCanvas = this.convertImageToCanvas(
          qrCodeWrapper.children[1]
        );

        const imgWidth = this.size / 2;
        const imgHeight =
          (this.size * brandImage.height) / brandImage.width / 3;
        const ctx = qrCodeCanvas.getContext("2d");

        ctx.drawImage(
          brandImage,
          (this.size - imgWidth) / 2,
          (this.size - imgHeight) / 2,
          imgWidth,
          imgHeight
        );

        this.$refs.qr.replaceWith(qrCodeCanvas);
      });

      brandImage.src = require(`@/assets/${this.brandImageSrc}`);
    },

    renderQRCodeinto(wrapper) {
      this.qrCode = new QRCode(wrapper, {
        text: this.text,
        width: this.size,
        height: this.size,
        colorDark: this.colorDark,
        colorLight: this.colorLight,
        correctLevel: QRCode.CorrectLevel[this.errorLevel]
      });
    },
    convertImageToCanvas(image) {
      var canvas = document.createElement("canvas");
      canvas.width = image.width;
      canvas.height = image.height;
      canvas.getContext("2d").drawImage(image, 0, 0);

      return canvas;
    }
  }
};
</script>
