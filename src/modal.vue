<script>
    /* global window */
    const $ = typeof window.jQuery === "undefined"
        ? require('jquery')
        : window.jQuery;
    if (typeof $.fn.modal === "undefined") {
        throw new Error("Bootstrap's modal.js not loaded");
    }
    export default {
        props: {
            // Whether to show the modal
            value: {
                type: Boolean,
                'default': false,
            },
            title: {
                type: String,
                'default': ''
            },
            small: {
                type: Boolean,
                'default': false
            },
            large: {
                type: Boolean,
                'default': false
            },
            closeByBackdrop: {
                type: Boolean,
                'default': true
            },
            showCloseButton: {
                type: Boolean,
                'default': true,
            },
            showCancelButton: {
                type: Boolean,
                'default': true,
            },
            okText: {
                type: String,
                'default': 'OK'
            },
            cancelText: {
                type: String,
                'default': 'Cancel'
            },
            okClass: {
                type: String,
                'default': 'btn btn-success'
            },
            cancelClass: {
                type: String,
                'default': 'btn btn-danger'
            },
            closeWhenOk: {
                type: Boolean,
                'default': false
            },
            showHeader: {
                type: Boolean,
                'default': true,
            },
            showFooter: {
                type: Boolean,
                'default': true,
            },
        },
        data () {
            return {};
        },
        computed: {
            modalClass () {
                return {
                    'modal-lg': this.large,
                    'modal-sm': this.small,
                }
            }
        },
        mounted () {
            this.initialize(this.value);
        },
        watch: {
            value (value) {
                value ? this.show() : this.hide();
            }
        },
        methods: {
            ok () {
                this.$emit('ok');
                if (this.closeWhenOk) {
                    this.hide();
                }
            },
            cancel () {
                this.$emit('cancel');
                this.hide();
            },
            show () {
                $(this.$el).modal('show');
            },
            hide () {
                return $(this.$el).modal('hide');
            },
            initialize(toShow = false) {
                const $modal = $(this.$el)
                    .modal({
                        show: false,
                        backdrop: this.closeByBackdrop ? true : 'static',
                    })
                    .on('show.bs.modal', () => {
                        this.$emit('input', true);
                    })
                    .on('hide.bs.modal', () => {
                        this.$emit('input', false);
                    })
                    .on('shown.bs.modal', () => {
                        this.$emit('shown');
                    })
                    .on('hidden.bs.modal', () => {
                        this.$emit('hidden');
                    });
                if (toShow) {
                    // putting timeout as modal doesn't open without it
                    setTimeout(() => {
                        $modal.modal('show');
                    });
                }
            }
        }
    };
</script>

<template>
    <div class="modal fade" tabindex="-1" role="dialog">
        <div class="modal-dialog" :class="modalClass" role="document">
            <div class="modal-content">
                <div class="modal-header" v-if="showHeader">
                    <slot name="header">
                        <button v-if="showCloseButton" type="button" class="close" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                        </button>
                        <h4 class="modal-title">
                            <slot name="title">
                                {{title}}
                            </slot>
                        </h4>
                    </slot>
                </div>
                <div class="modal-body">
                    <slot></slot>
                </div>
                <div class="modal-footer" v-if="showFooter">
                    <slot name="footer">
                        <button type="button" :class="cancelClass" @click="cancel" v-if="showCancelButton">{{cancelText}}</button>
                        <button type="button" :class="okClass" @click="ok">{{okText}}</button>
                    </slot>
                </div>
            </div>
        </div>
    </div>
</template>
