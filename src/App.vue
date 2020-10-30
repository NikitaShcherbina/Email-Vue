<template>
  <v-app>
    <router-view>

    </router-view>
  </v-app>
</template>

<script>

import Home from "@/views/Home";
export default {
  name: 'App',

  components: {
    Home

  },

  data: () => ({
    //
  }),
};
</script>

<style lang="scss">
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  .container {
    width: 1280px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    position: relative;
  }
  p {
    margin-bottom: 0px!important;
  }
  span {
    font-weight: bold;
    font-size: 14px;
  }
  th {
    background:whitesmoke;
  }
  .left {
    margin-left: 50px;
  }
  .bold {
    margin-right: 50px;
    color: #000;
  }

  @media screen and (max-width: 1023px) {
    .home .container .search-holder {
      margin-bottom: 20px!important;
    }
    .result {
      p {
        font-size: 14px!important;
        margin-left: 13px!important;
        span {
          font-size: 18.5px!important;
        }
      }
    }
    thead {
      width: 100%;
      background: whitesmoke;
      border-bottom: 10px;
      border-bottom: thin solid rgba(0, 0, 0, 0.12);
      tr {
        width: 60%;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        height: 30px;
        th {
          flex-grow: 1;
          justify-content: center;
          align-items: center;
          height: auto!important;
          padding: 0 8px!important;
          border-bottom: 0px!important;
          position: relative;
          &:not(:last-of-type) {
            &:before {
              content: '';
              position: absolute;
              left: 100%;
              height: 100%;
              width: 1px;
              z-index: 1;
              background: #cccccc;
            }
          }
          &:first-of-type {
            span {
              margin-left: 5px!important;
            }
          }
          span {
            font-size: 11px!important;
          }
        }
      }
    }
    table {
      display: flex;
      flex-direction: column;
      tbody {
        tr {
          display: flex;
          flex-direction: column;
          flex-wrap: wrap;
          border-bottom: thin solid rgba(0, 0, 0, 0.12);
          width: 100%;
          height: 83px;
          position: relative;
          .mail {
            position: absolute;
            bottom: 41px;
            left: 17px;
            width: 11px;
          }
          td {
            border-bottom: none!important;
            height: calc(100% / 4) !important;
            svg {
              right: 80.5%!important;
            }
            img {
              display: block!important;
            }
            p {
              margin-left: 10px;
            }
            .date {
              font-weight: normal!important;
            }
            .toMatch {
              width: 18px!important;
              line-height: 17px!important;
              border-radius: 3px;
              height: 16px!important;
              font-size: 12px;
              font-weight: bold;
            }
            &:first-of-type {
              font-weight: bold;
              padding-left: 40px!important;
              margin-top: 7px!important;
            }
            &:nth-of-type(2) {
              padding-left: 30px!important;
              margin-bottom: 5px;
            }
            &:nth-of-type(3) {
              padding-left: 5px!important;
              max-width: 80%;
              white-space: nowrap;
              overflow: hidden;
              svg {
                overflow: visible!important;
              }
              p {
                text-overflow: ellipsis;
                overflow: hidden;
                display: block!important;
              }
            }
            &:nth-of-type(4), svg {
              display: flex;
              align-items: center;
              p {
                margin-right: 5px;
              }
            }
            &:last-of-type {
              position: absolute;
              right: 0;
              top: 8px;
            }
          }
        }
      }
    }
  }
}


</style>
