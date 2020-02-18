# Using Pitaya-Link with DAP.js

## Introduction

[DAP.js](https://github.com/ARMmbed/dapjs) is a JavaScript interface to [CMSIS-DAP](https://www.keil.com/pack/doc/CMSIS/DAP/html/index.html), enabling access to Arm Microcontrollers using [Node.js](https://nodejs.org/) or in the browser using [WebUSB](https://wicg.github.io/webusb/).

This page demonstrates the flash exmaple using DAP.js.

Refer to the [DAP.js API Documentation](https://armmbed.github.io/dapjs/) for more information.

<div id="drop">
	<svg id="icon" xmlns="http://www.w3.org/2000/svg" width="50" height="43" viewBox="0 0 50 43">
        <path d="M48.4 26.5c-.9 0-1.7.7-1.7 1.7v11.6h-43.3v-11.6c0-.9-.7-1.7-1.7-1.7s-1.7.7-1.7 1.7v13.2c0 .9.7 1.7 1.7 1.7h46.7c.9 0 1.7-.7 1.7-1.7v-13.2c0-1-.7-1.7-1.7-1.7zm-24.5 6.1c.3.3.8.5 1.2.5.4 0 .9-.2 1.2-.5l10-11.6c.7-.7.7-1.7 0-2.4s-1.7-.7-2.4 0l-7.1 8.3v-25.3c0-.9-.7-1.7-1.7-1.7s-1.7.7-1.7 1.7v25.3l-7.1-8.3c-.7-.7-1.7-.7-2.4 0s-.7 1.7 0 2.4l10 11.6z"/>
    </svg>
	<input id="file" type="file" />
	<label id="label" for="file">Drag and drop a firmware image here</label>
	<div id="select">
	    <button id="button">Select Device</button>
	</div>
	<div id="status">
	    <div id="bar"></div>
	    <div id="transfer"></div>
	</div>
</div>
<script>
    let dropEl = document.getElementById("drop");
    let fileEl = document.getElementById("file");
    let selectEl = document.getElementById("select");
    let buttonEl = document.getElementById("button");
    let labelEl = document.getElementById("label");
    let statusEl = document.getElementById("status");
    let transferEl = document.getElementById("transfer");
    let barEl = document.getElementById("bar");

    let buffer = null;

    function setStatus(state) {
        labelEl.textContent = state;
    }

    function setTransfer(progress) {
        if (!progress) {
            statusEl.style.visibility = "hidden";
            return;
        }
        selectEl.style.visibility = "hidden";
        statusEl.style.visibility = "visible";
        barEl.style.width = `${progress * 100}%`;
        transferEl.textContent = `${Math.ceil(progress * 100)}%`;
    }

    // Load a firmware image
    function setImage(file) {
        if (!file) return;

        const reader = new FileReader();
        reader.onloadend = function(evt) {
            buffer = evt.target.result;
            setStatus(`Firmware image: ${file.name}`);
            selectEl.style.visibility = "visible";
        }
        reader.readAsArrayBuffer(file);
    }

    // Choose a device
    function selectDevice() {
        setStatus("Selecting device...");
        setTransfer();

        navigator.usb.requestDevice({
            filters: [{vendorId: 0xD28}]
        })
        .then(device => update(device))
        .catch(error => {
            statusEl.style.visibility = "hidden";
            setStatus(error);
        });
    }

    // Update a device with the firmware image
    function update(device) {
        if (!buffer) return;

        const transport = new DAPjs.WebUSB(device);
        const target = new DAPjs.DAPLink(transport);

        target.on(DAPjs.DAPLink.EVENT_PROGRESS, progress => {
            setTransfer(progress);
        });

        // Push binary to board
        return target.connect()
        .then(() => {
            setStatus(`Flashing binary file ${buffer.byteLength} words long...`);
            return target.flash(buffer);
        })
        .then(() => {
            setStatus("Disconnecting...");
            return target.disconnect();
        })
        .then(() => {
            setStatus("Flash complete!");
            setTransfer();
            fileEl.value = "";
        })
        .catch(error => {
            statusEl.style.visibility = "hidden";
            setStatus(error);
        });
    }

    fileEl.addEventListener("change", event => {
        setImage(event.target.files[0]);
    });

    dropEl.addEventListener("drop", event => {
        setImage(event.dataTransfer.files[0]);
    });

    buttonEl.addEventListener("click", selectDevice);

    ["drag", "dragstart", "dragend", "dragover", "dragenter", "dragleave", "drop"].forEach(eventName => {
        dropEl.addEventListener(eventName, event => {
            event.preventDefault();
            event.stopPropagation();
        });
    });

    ["dragover", "dragenter"].forEach(eventName => {
        dropEl.addEventListener(eventName, event => {
            dropEl.classList.add("hover");
        });
    });

    ["dragleave", "dragend", "drop"].forEach(eventName => {
        dropEl.addEventListener(eventName, event => {
            dropEl.classList.remove("hover");
        });
    });
</script>


## Create an Issue

Interested in contributing to this project? Want to report a bug? Feel free to click here:

<a href="https://github.com/makerdiary/pitaya-link/issues/new?title=DAPjs%20Usage:%20%3Ctitle%3E"><button data-md-color-primary="red-bud"><i class="fa fa-github"></i> Create an Issue</button></a>